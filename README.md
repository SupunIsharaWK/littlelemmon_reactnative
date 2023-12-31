# Little Lemon Food Ordering App

- The application is a React Native Expo Food app.
- Users can sign up on the Little Lemon restaurant app.
- Users will have to go through a registration process.
- Once they complete that phase, they are redirected to a home screen.
- After completing the onboarding flow, the home screen will represent the landing screen, displaying a header, a banner with a search bar and a list of menu items where a user can filter each category.
- User can also customize their name, email, photo and other user preferences through a Profile Screen.
- The profile screen also contains four checkboxes that enable specific email notifications, like order status, password changes, special offers, and newsletters.
- Use the AsyncStorage module to preserve the chosen preferences even when the user quits the application
- When clicking the Logout button, the user will be redirected back to the login page, clearing all data saved from the Profile.
- Use SQLite Database to populate, query and filter menu items.

## Table of contents

- [Overview](#overview)
  - [How to use the project](#how-to-use-the-project)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Useful resources](#useful-resources)

## Overview

### How to use the project

##### npm install && npm start
##### Then, a QR Code will appear on your terminal.

### Screenshot
![final_mockup](https://user-images.githubusercontent.com/108392678/217717918-a6f83c94-c1ab-4796-903e-388b9a67cdd9.jpg)
![Onboarding](https://user-images.githubusercontent.com/108392678/217715066-19026169-ab51-450e-b21c-cc925940d03e.jpg)
![Profile and Home](https://user-images.githubusercontent.com/108392678/217715079-d66eb960-f5cf-4cdf-8f33-b45b320fca7e.jpg)

### Links

- Github: [Code](https://github.com/marventures/little-lemon-app)
- Demo : Scan the [QR Code](https://expo.dev/@marventures/little-lemon-app) to see the demo.

## My process

### Built with

- [React Native](https://reactnative.dev/docs/environment-setup) - React Native app built with expo
- [SQLite](https://docs.expo.dev/versions/latest/sdk/sqlite/) - For storing the restaurant's menu items.
- [AsyncStorage](https://react-native-async-storage.github.io/async-storage/docs/api/) - For storing user preferences.
- [StyleSheet](https://reactnative.dev/docs/stylesheet) - For styles

### What I learned

- Create a React Native App using Expo
- Create a wireframe and high-fidelity mockup using Figma.
- Use ContextAPI for login
- Use React Navigation (Native Stack) for screen routes.
- Use ImagePicker API to set user Profile Picture
- Use use fonts Hook from expo-fonts to set custom fonts
- Use AsyncStorage to store user settings.
- Use getItem and setItem methods to read and set data to AsyncStorage
- ConnectAsyncStorage to a state
- Use SQLite to store Menu Items
- Connect SQLite to a state
- Create form validation for users
- Handling side-effects using useEffect Hook
- Use the FlatList component to render the menu
- Use the ScrollView component to render the categories' title
- Use View, View, Text Components
- Extract all styles to StyleSheet API

Here is a code snippet:

```jsx
const [profile, setProfile] = useState({
  firstName: "",
  lastName: "",
  email: "",
  phoneNumber: "",
  orderStatuses: false,
  passwordChanges: false,
  specialOffers: false,
  newsletter: false,
  image: "",
});
const [data, setData] = useState([]);
const [searchBarText, setSearchBarText] = useState("");
const [query, setQuery] = useState("");
const [filterSelections, setFilterSelections] = useState(
  sections.map(() => false)
);

const fetchData = async () => {
  try {
    const response = await fetch(API_URL);
    const json = await response.json();
    const menu = json.menu.map((item, index) => ({
      id: index + 1,
      name: item.name,
      price: item.price.toString(),
      description: item.description,
      image: item.image,
      category: item.category,
    }));
    return menu;
  } catch (error) {
    console.error(error);
  } finally {
  }
};

useEffect(() => {
  (async () => {
    let menuItems = [];
    try {
      await createTable();
      menuItems = await getMenuItems();
      if (!menuItems.length) {
        menuItems = await fetchData();
        saveMenuItems(menuItems);
      }
      const sectionListData = getSectionListData(menuItems);
      setData(sectionListData);
      const getProfile = await AsyncStorage.getItem("profile");
      setProfile(JSON.parse(getProfile));
    } catch (e) {
      Alert.alert(e.message);
    }
  })();
}, []);
```

### Useful resources

- [React Native Docs (StyleSheet) ](https://reactnative.dev/docs/stylesheet) - This helped me with all the necessary React Native styles. I liked their documentation and will use it going forward.
- [ImagePicker API](https://docs.expo.dev/versions/latest/sdk/imagepicker/) - This helped me create an option for users to select profile pictures on their devices.
- [SQLite](https://docs.expo.dev/versions/latest/sdk/sqlite/) - This helped me save menu items.
- [Async Storage](https://react-native-async-storage.github.io/async-storage/docs/api/) - This helped me save user settings.
- [ContextAPI](https://beta.reactjs.org/reference/react/createContext)- This helped me create an authentication context for login.
