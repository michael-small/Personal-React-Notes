# Component Recipees

I return to my previous code across a lot of projects of mine often. Here are some samples of components or other concepts that I can/have re-used.

Indentations of component layouts are parent/child relations.

## Searchbar

**WORK IN PROGRESS**

*Components*
* `Cockpit FC`
  * `SearchBar FC`
  * `Items FC`

`Cockpit FC`
```jsx
export default function Cockpit(props) {
	const ITEMS = props.ITEMS;
	const [searchQuery, setSearchQuery] = useState('');
	const filterediTEMS = filterItems(items, searchQuery);

	return (
    <div>
			<Search search={searchQuery} updateSearch={setSearchQuery} />
			<Items items={filteredItems} />
		</div>
	);
}
```
