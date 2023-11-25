# React Admin P1

##### React-Admin tutorial notes

Create new project and install packages

```javascript
yarn create react-app test-admin
cd test-admin/
yarn add react-admin ra-data-json-server prop-types
```

Edit file src/App.js

```javascript
import * as React from "react";
import { Admin, Resource } from 'react-admin';
import jsonServerProvider from 'ra-data-json-server';

import { ListGuesser } from 'react-admin';

const App = () => {
  const dataProvider = jsonServerProvider('https://jsonplaceholder.typicode.com');
  return(
    <Admin dataProvider={dataProvider}>
      <Resource name="users" list={ListGuesser} />
    </Admin>
  );
}

export default App;
```
<!--more-->
###### Add dashboard page

1. Create dashboard component
2. Set <Admin **dashboard**={ Dashboard } ...>

###### Customizing menu icon
1. Import Icon
2. <Resource **icon**={ ICON } ...>

###### Adding login page
1. Create src/Providers/authProvider (Example code: ...)
2. <Admin authProvider={ authProvider } ...>

###### Check screen size
```javascript
const isSmall = useMediaQuery(theme => theme.breakpoints.down('sm'));
```
