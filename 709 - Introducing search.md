Introducing Search APIs (709)

# Overview
- Developers choose what to index via Search APIs
- App results appear in both Spotlight *and Safari*
- Public deeplinks will show up for apps the user hasn’t installed
# App / Content Discovery
1. Content indexed in devices that is marked as public gets promoted to the cloud index based on amount of usage/engagement
2. Content is also scraped from app websites
# App Search API
## NSUserActivity
Extension of the iOS 8 handoff API. As you expose NSUserActivities past behavior gets automatically indexed
## CoreSpotlight
Manually expose app content. Best way to index private content.
## Web markup
Apps that mirror content on website, can be marked up so they get scraped and deep links work
# NSUserActivity
- Capture application state for use in handoff
- New in iOS 9
	- Add indexable metadata
	- Activities can be designated as searchable
	- Results show up in search
## Usage
Track content that user has viewed, with metadata that will help index the content.
## API usage
### Capability flags
`eligibleForHandoff`, `eligibleForSearch`, `eligibleForPublicIndexing`
### Indexed Properties
`title`, `keywords`, `contentAttributeSet: CSSearchableItemAttributeSet?`, `expirationDatae`
### Web URL
`webpageURL` if its possible to resume from website set this
### Continue
`application:continueUserActivity:userInfo:`
### Public Indexing
NSUserActivity can be marked as public indexing, if so every time the user “interacts” with the content it increases rank until its promoted to “cloud index”

One way hash of every activity is sent to cloud index and then after threshold the public item is shared. For privacy but also filtering for interest
### Benefits
- Will get siri suggestions and reminders (“remind me about this”)
- Handoff
# CoreSpotlight
## API
### CSSearchableItem
Collection of item attributes (CSSearchableItemAttributeSet) to index
### CSSearchableItemAttributeSet
Attributes that are indexed/displayed by spotlight
### CSSearchableIndex
Collection of CSSearchableItem(s) added to device index
## Restoration
Uses the same api as the handoff api
# Web Markup
Powered by Applebot, crawls the web and provides search results for deep links (I think this is based on smart banner tags since they said this already works)
## Enable app search
1. Markup mobile web for deep links (submit as support/marketing url with app)
2. Ensure app can handle deep links
3. Add additional markup for structured results to improve search result UI
## Universal links
Unique since its identified by domain/website, secure, flexible.  Register the links in app and then markup the pages with the tags via smart app banner/“other standards”
## Third party support
Supports twitter cards and facebook app links. Handles og:image/audio/video markup for structured data to improve appearance of results. They support lots of this.
# Achieving Best Results
## Relevance
Important attribute of ranking is the amount of interaction
1. URL popularity (relevance score) 
2. Activities (NSUserActivity)
3. Engagements - When search result is presented
Should have 3-5 Keywords per item, include aliases or common nicknames