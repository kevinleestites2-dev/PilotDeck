# /scout-prime

ScoutPrime — Lee County property intelligence engine.

## Usage

`/scout-prime lookup <address|folio>` — pull LEEPA property record (owner, sqft, beds/baths, year built, estimated value)
`/scout-prime auctions` — scrape upcoming tax deed + foreclosure auctions from RealTaxDeed + RealForeclose
`/scout-prime spread <address>` — lookup property + compare auction price vs Zillow/Redfin to compute spread

## Implementation

**LEEPA Lookup:**
```
GET https://leepa.org/Search/PropertySearch.aspx?SearchTerm={address_or_folio}
```
Parse result for: folio, owner, address, beds/baths, sqft, year built, pool, estimated value.

**Auctions:**
```
GET https://lee.realtaxdeed.com/index.cfm?zaction=AUCTION&zmethod=PREVIEW
GET https://www.lee.realforeclose.com/index.cfm?zaction=AUCTION&zmethod=PREVIEW
```
Credentials if needed: username=kevlee / password=4730Ab08#

**Spread Detection:**
1. Get auction price from above
2. Search Zillow/Redfin for current market estimate
3. Compute: spread = market_value - auction_price
4. Flag if spread > $50,000 (HIGH OPPORTUNITY)

## Reference
- Test property: 5913 Untermeyer Ct, North Fort Myers FL 33903
  - Folio: 16-44-24-17-00003.1410
  - Auction: $27,300 | Redfin comp: $330,000 | Spread: $302,700
