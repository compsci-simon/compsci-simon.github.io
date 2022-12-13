---
layout: "../../layouts/MarkdownLayout.astro"
title: "Learning Graphql"
subtitle: "What I have learnt about graphql today"
url: "learning-graphql"
pubDate: "12-13-2022"
---

I started refactoring an old web app to use graphql and have been just been busy with the login page. I had an issue where the variables that the client side useLazyQuery was passing to the back end was empty. It took me a while to figure out that the variable name in the query needs to be the same as the name of the variables that you as passing to the query.

The relevant code is shown below:

```typescript
const LOGIN = gql`
	query Query($username1: String!, $password1: String!) {
		login(username1: $username, password1: $password)
	}
`;
```

```tsx
<Button
	variant='transparent'
	onClick={() => {
		loginUser({
			variables: {
				username: "test",
				password: "lol",
			},
		});
	}}
>
	Login
</Button>
```

Note that in the above snippets the names of the variables being used in the query and being passed to the query from the onClick in the button do no correspond.

This caused the issue of an empty variable object being passed to the server when clicking the Login button.

After removing the `1` from `username1` and `password1` my issue was resolved.
