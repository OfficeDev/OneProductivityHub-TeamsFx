## Part 4 - Design your One Productivity Hub by using Microsoft Graph Toolkit components

- [Part 0 - Environment Setup](00-Setup.md) 
- [Part 1 - Create a new Teams tab](01-Create_Teams_tab.md) 
- [Part 2 - Add Single Sign On feature in your tab](/Labs/02-Create_SSO_Feature.md)
- [Part 3 - Add Microsoft Graph Toolkit TeamsFX Provider and build consent permissions feature](/Labs/03-Initialize_MGT_and_consent_permissions.md)
- [Part 4 - Design your One Productivity Hub by using Microsoft Graph Toolkit components](04-Design_your_tab_using_MGT_components.md) ( **📍 You are here** )
- [Part 5 - Test One Productivity Hub app on Microsoft Teams](05-Test_your_tab.md)

Now, you're ready to add any of the Microsoft Graph Toolkit components to your tab.

### Design your tab with HTML and CSS
To make our tab look structured, we create three columns in a row by using some HTML and CSS code as the following:

1. Let's start with CSS. Add below CCS code in `src/components/App.css`:

    ```CSS
    body,
    #root>div {
        background-color: #F3F2F1;
    }      
    .features {
        min-height: 95vh;
        margin: 20px;
        background-color: #FFF;
        box-shadow: 0px 1.2px 3.6px rgba(0, 0, 0, 0.11), 0px 6.4px 14.4px rgba(0, 0, 0, 0.13);
        border-radius: 4px;
    }    
    .header {
        display: flex;
        background-color: #f0f0f0;
    } 
    .title {
        margin-top: 20;
        margin-left: 10;
        width: 100%;
    }        
    .title h2 {
        font-size: 24px;
        padding-left: 20;
        display: inline;
        font-weight: 600;   
    }        
    .title h3 {
        float: left;
        width: 32%;
        background:transparent;
        font-size: 16px;
        margin-bottom: 10;
        padding-left: 20;
        padding-top: 10;
        color: #8A8886;
        font-weight: 600;
    }     
    .auth {
        margin-top: 30vh;
        font-size: 18px;
        background-color: #eeeeee;    
    }
    .auth button {  
        font-size: 16px;
        text-align: center;
        display: block;
        margin: 32px auto;
    }        
    .auth h3 {
        margin-left: 10px;
        font-weight: 600;
        font-size: 24px;
        text-align: center;
    }
    .auth p {
        margin-left: 10px;
        font-size: 16px;
        text-align: center;
    }
    mgt-person {
        padding: 20;
        margin-left: 20;
        --avatar-size: 60px;
        --font-family: 'Segoe UI';
        --font-size: 20px;
        --font-weight: 700;
        --color: black;
        --text-transform: none; 
        --line2-font-size: 14px;
        --line2-font-weight: 400;
        --line2-color: #8A8886;
        --line2-text-transform: none;
    }
    .content, html, body {
        height: 98%;   
        }
    .mgt-col {
        float: left;
        width: 32%;
        background:transparent;
        height:500px;
        overflow: hidden;
        padding: 10;
        }
    .mgt-col:hover {
        overflow-y: auto;
        }
    ```
1. Add the following import on top of `Tab.jsx` under `src/components` folder:

    ```javascript
    import {  Agenda, Todo, FileList, Person, PersonViewType } from '@microsoft/mgt-react';
    ```
    
1. In `Tab.jsx`, add the following HTML in **return()** under **render()** to show One Productivity Hub app when permission consent is completed:

    ```html
    {this.state.showLoginPage === false && 
    <div>
        <div className='features-avatar'>
        </div>
        
        <div className="features">
        </div>
    </div>
    }
    ```

### Person component

In `Tab.jsx` under **return()**, add the Person component inside the div tagged with `className="features-avatar"`:

```html
<Person personQuery="me" view={PersonViewType.threelines}></Person>
```

### Add title and column for each feature in One Productivity Hub
To make our tab look structured, let's create titles and  columns that will be added in the One Productivity Hub moving forward. In `Tab.jsx` under **return()**, add the following html inside the div tagged with `className="features"`:

```HTML
<div className="header"><div className="title">
    <h2>One Productivity Hub</h2>
    <div class="row">
        <div class="column"><h3>Calendar events</h3></div>
        <div class="column"><h3>To-do tasks</h3></div>
        <div class="column"><h3>Files</h3></div>
    </div>
</div></div>

<div class="row" className="content">
    <div class="column" className="mgt-col"></div>
    <div class="column" className="mgt-col"></div>
    <div class="column" className="mgt-col"></div>
</div>
```

#### Agenda component

Under div tagged with `className="content"`, add the Agenda component inside the first column div:

```HTML
<Agenda></Agenda>
```

#### To-do component

Under div tagged with `className="content"`, add the To-do component inside the second column div:

```HTML
<Todo></Todo>
```

#### FileList component

Under div tagged with `className="content"`, add the FileList component inside the third column div:

```HTML
<FileList></FileList>
```

### Final version of `Tab.jsx`
Finally, `Tab.jsx` will look as following:
```javascript
import React from 'react';
import './App.css';
import { TeamsFx } from "@microsoft/teamsfx";
import { Button } from "@fluentui/react-northstar"
import { Providers, ProviderState } from '@microsoft/mgt-element';
import { TeamsFxProvider } from '@microsoft/mgt-teamsfx-provider';
import { CacheService } from '@microsoft/mgt';
import {  Agenda, Todo, FileList, Person, PersonViewType } from '@microsoft/mgt-react';

class Tab extends React.Component {

  constructor(props) {
    super(props);
    CacheService.clearCaches();

    this.state = {
      showLoginPage: undefined,
    }
  }

  async componentDidMount() {

    /*Define scope for the required permissions*/
    this.scope = [
      "User.Read",
      "User.ReadBasic.All",
      "Calendars.Read",
      "Files.Read",
      "Files.Read.All",
      "Sites.Read.All",
      "Tasks.Read",
      "Tasks.ReadWrite",
      "People.Read",
      "User.ReadBasic.All"
    ];

    /*Initialize TeamsFX provider*/
    this.teamsfx = new TeamsFx();
    const provider = new TeamsFxProvider(this.teamsfx, this.scope)
    Providers.globalProvider = provider;
   
    /*Check if consent is needed*/
    let consentNeeded = false;
    try {
      await this.teamsfx.getCredential().getToken(this.scope);
    } catch (error) {
      consentNeeded = true;
    }
    this.setState({
      showLoginPage: consentNeeded
    });
    Providers.globalProvider.setState(consentNeeded ? ProviderState.SignedOut : ProviderState.SignedIn);
    return consentNeeded;

  }

  async loginBtnClick() {
    try {
      await this.teamsfx.login(this.scope);
      Providers.globalProvider.setState(ProviderState.SignedIn);
      this.setState({
        showLoginPage: false
      });
    } catch (err) {
      if (err.message?.includes("CancelledByUser")) {
        const helpLink = "https://aka.ms/teamsfx-auth-code-flow";
        err.message += 
          "\nIf you see \"AADSTS50011: The reply URL specified in the request does not match the reply URLs configured for the application\" " + 
          "in the popup window, you may be using unmatched version for TeamsFx SDK (version >= 0.5.0) and Teams Toolkit (version < 3.3.0) or " +
          `cli (version < 0.11.0). Please refer to the help link for how to fix the issue: ${helpLink}` ;
      }

      alert("Login failed: " + err);
      return;
    }
  }


  render() {
    return (
      <div>
        {this.state.showLoginPage === false && 
        <div>

          <div className='features-avatar'>
            <Person personQuery="me" view={PersonViewType.threelines} ></Person>
          </div>
          
              <div className="features">
                <div className="header"><div className="title">
                    <h2>One Productivity Hub</h2>
                    <div class="row">
                    <div class="column"><h3>Calendar events</h3></div>
                    <div class="column"><h3>To-do tasks</h3></div>
                    <div class="column"><h3>Files</h3></div>
                        </div>
                    </div>
                </div>

                <div class="row" className="content">
                    <div class="column" className="mgt-col">
                        <Agenda></Agenda>
                    </div>
                    <div class="column" className="mgt-col">
                        <Todo></Todo>
                    </div>
                    <div class="column" className="mgt-col">
                        <FileList></FileList>
                    </div>                    
                </div>
            </div>
        </div>
           
        }
        {
        this.state.showLoginPage === true && 
        <div className="auth">
        <h3>Welcome to One Productivity Hub app!</h3>
        <p>Please click on "Start One Productivity Hub" and consent permissions to use the app.</p> 
        <Button primary onClick={() => this.loginBtnClick()}>Start One Productivity Hub</Button>
        </div>
        }
      </div>
      
    );
  }
}
export default Tab;
```


## References
- Microsoft Docs - [Build a Microsoft Teams tab with the Microsoft Graph Toolkit](https://cda.ms/1Jh)

## Next Step
> ▶️ **[Part 5 - Test One Productivity Hub app on Microsoft Teams](05-Test_your_tab.md)**
