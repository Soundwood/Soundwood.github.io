---
layout: post
title:      "Final Project: The Edge Details"
date:       2020-11-11 21:48:44 +0000
permalink:  final_project_the_edge_details
---


For the final react-redux project I chose to make a tool that I wish I had available when I first started looking for homes. That is an analysis on how much home I can reasonably afford. There are several “Rules” for determining this though all of them are based on only a few variables. By asking the user for this information, I could then generate solutions to each of the analysis to be presented to the user at the same time. No need to keep redoing the same math over and over again. 

Below are some of the more fringe issues and discoveries I experienced while building this project. You may not encounter any of these but perhaps if you do this will be a good resource.

## Scrolled to Middle of Page after following a Link component

The default state for rendering a new page when following a Link component is to stay at the same relative scroll position. Since this position is relative, the user could click a link and end up on a new page scrolled near the middle or bottom. Not a great user experience. The below solution automatically scrolls to the top of the page on a page update. 
>https://reactrouter.com/web/guides/scroll-restoration

	class ScrollToTop extends Component {
	  componentDidUpdate(prevProps) {
	    if (this.props.location !== prevProps.location) {
	      window.scrollTo(0, 0)
	    }
	  }
	  render() {
	    return this.props.children
	  }
	}

	export default withRouter(ScrollToTop)
	Then render it at the top of your app, but below Router:

	const App = () => (
	  <Router>
	    <ScrollToTop>
	      <App/>
	    </ScrollToTop>
	  </Router>
	)

A more bespoke solution would be to use the javascript command

	window.scrollTo(x-coord, y-coord)
	
as needed such as within certain Link buttons.

## Data Validations Before Fetching to API

Because we like to keep input from forms in state (i.e. controlled), we have the ability to quickly check the values to determine if they are valid prior to submitting them to the backend. Furthermore we can do things like enabling or disabling the ‘submit’ buttons until all the values in the form are valid Thus preventing the user from sending something we already know will not be accepted by the backend/api. The following is a great breakdown on how to implement this.
>https://goshakkk.name/instant-form-fields-validation-react/ 

Generally we want to create a function that returns an object with each input value checked for validity. If a specific input is invalid we can then let the user know visually by say wrapping the input field with a red border. If any of the input values are invalid we can disable the submit button. 

## Hitting the Action function but not the Reducer

I'll admit this one had me stumped for a while. I had imported the function and included it in the connect statement as shown below. However, I neglected to add the function as part of my const declaration line. This resulted in me hitting the function but skipping the dispatch which normally leads to the reducer. 

Right:

	import { deleteScenario } from  '../actions/scenarios'
	const  ScenarioCard = ({ scenario, deleteScenario, history}) => {
		stuff
	}
	export  default  connect(null, {deleteScenario})(ScenarioCard)

Wrong:

	import { deleteScenario } from  '../actions/scenarios'
	const  ScenarioCard = ({ scenario, DELETESCENARIO IS MISSING HERE, history}) => {
		stuff
	}
	export  default  connect(null, {deleteScenario})(ScenarioCard)


## Aspirations versus Available Time

I originally had much larger goals for this project. Hopefully I will have the time in the coming weeks to bring some of them to fruition. As a friendly reminder if you are in a similar situation, don’t be discouraged when things take longer than anticipated. Creating something from nothing always takes time.
