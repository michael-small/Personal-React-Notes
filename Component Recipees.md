# Component Recipees

I return to my previous code across a lot of projects of mine often. Here are some samples of components or other concepts that I can/have re-used.

Indentations of component layouts are parent/child relations.

## Searchbar

*Components*
* `Cockpit FC`
  * `SearchBar FC`
  * `Items FC`

#### Explanation:

1) Parent component (`Cockpit FC`) passes a `useState` hook's value and setter to `Search FC`. 
2) Search's text field has an `onChange` that evokes the parents hook state setter.
3) Parent `Cockpit FC` filters by the pased up search query.
4) `Items FC` only maps over items that passed the filter.

`Cockpit FC`
```jsx
const filterItems = (items, searchQuery) => {
	if (!searchQuery) {
		return items;
	}

	return items.filter((item) => {
		const itemName = item.{some_field}.toLowerCase();
		return (
			itemName.toLowerCase().indexOf(searchQuery.toLowerCase()) !== -1
		);
	});
};

export default function Cockpit(props) {
	const items = props.items;
	const [searchQuery, setSearchQuery] = useState('');
	const filteredItems= filterItems(items, searchQuery);

	return (
    		<div>
			<Search search={searchQuery} updateSearch={setSearchQuery} />
			<Items items={filteredItems} />
		</div>
	);
}
```

`Search FC`
```jsx
export default function Search(props) {
	return (
		<div>
			<TextField
				label='Search by item {some_field}'
				type='text'
				value={props.search}
				onChange={(event) => props.updateSearch(event.target.value)}
			/>
		</div>
	);
}
```
#### Example from my Ed's Garage Sale project: 

* [`Cockpit FC`](https://github.com/michael-small/Eds-Garage-Sale/blob/master/client/src/components/Cockpit/Cockpit.js)
* [`Search FC`](https://github.com/michael-small/Eds-Garage-Sale/blob/master/client/src/components/Search/Search.js)
* [`Items FC`](https://github.com/michael-small/Eds-Garage-Sale/blob/master/client/src/components/Cockpit/Listings/Listings.js)
