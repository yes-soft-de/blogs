# Schemas for SEO

SEO consists of many many factors, you know the usual On-Page SEO, Off-Page SEO and a whole bunch of optimizing the heck of the website. yet, there is, however, a good method of making a good SEO to your website AND help the developers doing there job.



## Standardizing ECommerce Products

Let's take 2 examples of a website and we shall interduce what we want to do next.

### Fashions Ecommerce Website

Let's say we have a fashion website, this site provide fashion choices.

Now if we tried to count the properties of such a product there would be for example:

1. Size
2. Color
3. Barcode
4. Name
5. ...

while this should be done during the UX phase, we can miss something. Now say we wanted to standardize those across all websites, wouldn't it be wonderful? this way the Crawlers could extract the information faster and more reliably. 

### Painting Ecommerce Website

Let's say we have a art gallery looking to sell paintings, something like Ishtar-art.de, now this is a bit trickier than the previous example for 2 reasons, because when the design gets more and more elaborate, it's REALLY hard for us to extract information from an HTML code, and if it is hard for us, you can bet it's hard for crawlers. AND there is a huge opportunity to miss some important details from your DB. Something like the license, the creation date ...

Plus one more thing, in the end, can't you count paintings as a product like a Jeans, I mean sure there is an extremely limited supply for this type of product. BUT in the end it is soled just like a regular jeans!

Wouldn't it be wonderful to categorize all kind of product across all sites that deals with art, fashion chairs and what not? Well google and many others noticed this, and they fixed it.



## Introducing Schemas

In essence the Schemas are a guide lines published by [schema.org](https://scemas.org) and it contains most of the products you can sell online if not all. This includes but not limited to houses, cars, games, books, your store and more.

For our proposes though we are going to access the 2 examples above and we shall search for a  convenient schema to rely on, in our site.

First lets start with the Fashion store, we shall start with the more specific Schemas and get less and less focused until we find a good resolution.

after a few minutes searching it appears that a product is a good search term and in this search we found 3 good resolutions for our purposes being:

1.  [Individual Product](https://schema.org/IndividualProduct )

    A single, identifiable product instance (e.g. a laptop with a particular serial number). 

2. [Product Model]( https://schema.org/ProductModel )

    A datasheet or vendor specification of a product (in the sense of a prototypical description). 

3. [Product](https://schema.org/Product)
	
	Any offered product or service. For example: a pair of shoes; a concert ticket; the rental of a car; a haircut; or an episode of a TV show streamed online.
	

OK, that seems to fit our criteria, and we shall use Product in our Project. that said the full details this schema entails are:

| Property                                              | Expected Type                                                | Description                                                  |
| :---------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Properties from [Product](https://schema.org/Product) |                                                              |                                                              |
| `additionalProperty`                                  | [PropertyValue](https://schema.org/PropertyValue)            | A property-value pair representing an additional characteristics of the entitity, e.g. a product feature or another characteristic for which there is no matching property in schema.org.  Note: Publishers should be aware that applications designed to use specific schema.org properties (e.g. http://schema.org/width, http://schema.org/color, http://schema.org/gtin13, ...) will typically expect such data to be provided using those properties, rather than using the generic property/value mechanism. |
| `aggregateRating`                                     | [AggregateRating](https://schema.org/AggregateRating)        | The overall rating, based on a collection of reviews or ratings, of the item. |
| `audience`                                            | [Audience](https://schema.org/Audience)                      | An intended audience, i.e. a group for whom something was created. Supersedes [serviceAudience](https://schema.org/serviceAudience). |
| `award`                                               | [Text](https://schema.org/Text)                              | An award won by or for this item. Supersedes [awards](https://schema.org/awards). |
| `brand`                                               | [Brand](https://schema.org/Brand) or [Organization](https://schema.org/Organization) | The brand(s) associated with a product or service, or the brand(s) maintained by an organization or business person. |
| `category`                                            | [PhysicalActivityCategory](https://schema.org/PhysicalActivityCategory) or [Text](https://schema.org/Text) or [Thing](https://schema.org/Thing) or [URL](https://schema.org/URL) | A category for the item. Greater signs or slashes can be used to informally indicate a category hierarchy. |
| `color`                                               | [Text](https://schema.org/Text)                              | The color of the product.                                    |
| `depth`                                               | [Distance](https://schema.org/Distance) or [QuantitativeValue](https://schema.org/QuantitativeValue) | The depth of the item.                                       |
| `gtin`                                                | [Text](https://schema.org/Text)                              | A Global Trade Item Number ([GTIN](https://www.gs1.org/standards/id-keys/gtin)). GTINs identify trade items, including products and services, using numeric identification codes. The [gtin](https://schema.org/gtin) property generalizes the earlier [gtin8](https://schema.org/gtin8), [gtin12](https://schema.org/gtin12), [gtin13](https://schema.org/gtin13), and [gtin14](https://schema.org/gtin14) properties. The GS1 [digital link specifications](https://www.gs1.org/standards/Digital-Link/) express GTINs as URLs. A correct [gtin](https://schema.org/gtin) value should be a valid GTIN, which means that it should be an all-numeric string of either 8, 12, 13 or 14 digits, or a "GS1 Digital Link" URL based on such a string. The numeric component should also have a [valid GS1 check digit](https://www.gs1.org/services/check-digit-calculator) and meet the other rules for valid GTINs. See also [GS1's GTIN Summary](http://www.gs1.org/barcodes/technical/idkeys/gtin) and [Wikipedia](https://en.wikipedia.org/wiki/Global_Trade_Item_Number) for more details. Left-padding of the gtin values is not required or encouraged. |
| `gtin12`                                              | [Text](https://schema.org/Text)                              | The GTIN-12 code of the product, or the product to which the offer refers. The GTIN-12 is the 12-digit GS1 Identification Key composed of a U.P.C. Company Prefix, Item Reference, and Check Digit used to identify trade items. See [GS1 GTIN Summary](http://www.gs1.org/barcodes/technical/idkeys/gtin) for more details. |
| `gtin13`                                              | [Text](https://schema.org/Text)                              | The GTIN-13 code of the product, or the product to which the offer refers. This is equivalent to 13-digit ISBN codes and EAN UCC-13. Former 12-digit UPC codes can be converted into a GTIN-13 code by simply adding a preceeding zero. See [GS1 GTIN Summary](http://www.gs1.org/barcodes/technical/idkeys/gtin) for more details. |
| `gtin14`                                              | [Text](https://schema.org/Text)                              | The GTIN-14 code of the product, or the product to which the offer refers. See [GS1 GTIN Summary](http://www.gs1.org/barcodes/technical/idkeys/gtin) for more details. |
| `gtin8`                                               | [Text](https://schema.org/Text)                              | The [GTIN-8](http://apps.gs1.org/GDD/glossary/Pages/GTIN-8.aspx) code of the product, or the product to which the offer refers. This code is also known as EAN/UCC-8 or 8-digit EAN. See [GS1 GTIN Summary](http://www.gs1.org/barcodes/technical/idkeys/gtin) for more details. |
| `hasMerchantReturnPolicy`                             | [MerchantReturnPolicy](https://pending.schema.org/MerchantReturnPolicy) | Indicates a MerchantReturnPolicy that may be applicable. Supersedes [hasProductReturnPolicy](https://attic.schema.org/hasProductReturnPolicy). |
| `height`                                              | [Distance](https://schema.org/Distance) or [QuantitativeValue](https://schema.org/QuantitativeValue) | The height of the item.                                      |
| `isAccessoryOrSparePartFor`                           | [Product](https://schema.org/Product)                        | A pointer to another product (or multiple products) for which this product is an accessory or spare part. |
| `isConsumableFor`                                     | [Product](https://schema.org/Product)                        | A pointer to another product (or multiple products) for which this product is a consumable. |
| `isRelatedTo`                                         | [Product](https://schema.org/Product) or [Service](https://schema.org/Service) | A pointer to another, somehow related product (or multiple products). |
| `isSimilarTo`                                         | [Product](https://schema.org/Product) or [Service](https://schema.org/Service) | A pointer to another, functionally similar product (or multiple products). |
| `itemCondition`                                       | [OfferItemCondition](https://schema.org/OfferItemCondition)  | A predefined value from OfferItemCondition or a textual description of the condition of the product or service, or the products or services included in the offer. |
| `logo`                                                | [ImageObject](https://schema.org/ImageObject) or [URL](https://schema.org/URL) | An associated logo.                                          |
| `manufacturer`                                        | [Organization](https://schema.org/Organization)              | The manufacturer of the product.                             |
| `material`                                            | [Product](https://schema.org/Product) or [Text](https://schema.org/Text) or [URL](https://schema.org/URL) | A material that something is made from, e.g. leather, wool, cotton, paper. |
| `model`                                               | [ProductModel](https://schema.org/ProductModel) or [Text](https://schema.org/Text) | The model of the product. Use with the URL of a ProductModel or a textual representation of the model identifier. The URL of the ProductModel can be from an external source. It is recommended to additionally provide strong product identifiers via the gtin8/gtin13/gtin14 and mpn properties. |
| `mpn`                                                 | [Text](https://schema.org/Text)                              | The Manufacturer Part Number (MPN) of the product, or the product to which the offer refers. |
| `nsn`                                                 | [Text](https://schema.org/Text)                              | Indicates the [NATO stock number](https://en.wikipedia.org/wiki/NATO_Stock_Number) (nsn) of a [Product](https://schema.org/Product). |
| `offers`                                              | [Demand](https://schema.org/Demand) or [Offer](https://schema.org/Offer) | An offer to provide this item—for example, an offer to sell a product, rent the DVD of a movie, perform a service, or give away tickets to an event. Use [businessFunction](https://schema.org/businessFunction) to indicate the kind of transaction offered, i.e. sell, lease, etc. This property can also be used to describe a [Demand](https://schema.org/Demand). While this property is listed as expected on a number of common types, it can be used in others. In that case, using a second type, such as Product or a subtype of Product, can clarify the nature of the offer. Inverse property: [itemOffered](https://schema.org/itemOffered). |
| `productID`                                           | [Text](https://schema.org/Text)                              | The product identifier, such as ISBN. For example: `meta itemprop="productID" content="isbn:123-456-789"`. |
| `productionDate`                                      | [Date](https://schema.org/Date)                              | The date of production of the item, e.g. vehicle.            |
| `purchaseDate`                                        | [Date](https://schema.org/Date)                              | The date the item e.g. vehicle was purchased by the current owner. |
| `releaseDate`                                         | [Date](https://schema.org/Date)                              | The release date of a product or product model. This can be used to distinguish the exact variant of a product. |
| `review`                                              | [Review](https://schema.org/Review)                          | A review of the item. Supersedes [reviews](https://schema.org/reviews). |
| `sku`                                                 | [Text](https://schema.org/Text)                              | The Stock Keeping Unit (SKU), i.e. a merchant-specific identifier for a product or service, or the product to which the offer refers. |
| `slogan`                                              | [Text](https://schema.org/Text)                              | A slogan or motto associated with the item.                  |
| `weight`                                              | [QuantitativeValue](https://schema.org/QuantitativeValue)    | The weight of the product or person.                         |
| `width`                                               | [Distance](https://schema.org/Distance) or [QuantitativeValue](https://schema.org/QuantitativeValue) | The width of the item.                                       |
| Properties from [Thing](https://schema.org/Thing)     |                                                              |                                                              |
| `additionalType`                                      | [URL](https://schema.org/URL)                                | An additional type for the item, typically used for adding more specific types from external vocabularies in microdata syntax. This is a relationship between something and a class that the thing is in. In RDFa syntax, it is better to use the native RDFa syntax - the 'typeof' attribute - for multiple types. Schema.org tools may have only weaker understanding of extra types, in particular those defined externally. |
| `alternateName`                                       | [Text](https://schema.org/Text)                              | An alias for the item.                                       |
| `description`                                         | [Text](https://schema.org/Text)                              | A description of the item.                                   |
| `disambiguatingDescription`                           | [Text](https://schema.org/Text)                              | A sub property of description. A short description of the item used to disambiguate from other, similar items. Information from other properties (in particular, name) may be necessary for the description to be useful for disambiguation. |
| `identifier`                                          | [PropertyValue](https://schema.org/PropertyValue) or [Text](https://schema.org/Text) or [URL](https://schema.org/URL) | The identifier property represents any kind of identifier for any kind of [Thing](https://schema.org/Thing), such as ISBNs, GTIN codes, UUIDs etc. Schema.org provides dedicated properties for representing many of these, either as textual strings or as URL (URI) links. See [background notes](https://schema.org/docs/datamodel.html#identifierBg) for more details. |
| `image`                                               | [ImageObject](https://schema.org/ImageObject) or [URL](https://schema.org/URL) | An image of the item. This can be a [URL](https://schema.org/URL) or a fully described [ImageObject](https://schema.org/ImageObject). |
| `mainEntityOfPage`                                    | [CreativeWork](https://schema.org/CreativeWork) or [URL](https://schema.org/URL) | Indicates a page (or other CreativeWork) for which this thing is the main entity being described. See [background notes](https://schema.org/docs/datamodel.html#mainEntityBackground) for details. Inverse property: [mainEntity](https://schema.org/mainEntity). |
| `name`                                                | [Text](https://schema.org/Text)                              | The name of the item.                                        |
| `potentialAction`                                     | [Action](https://schema.org/Action)                          | Indicates a potential Action, which describes an idealized action in which this thing would play an 'object' role. |
| `sameAs`                                              | [URL](https://schema.org/URL)                                | URL of a reference Web page that unambiguously indicates the item's identity. E.g. the URL of the item's Wikipedia page, Wikidata entry, or official website. |
| `subjectOf`                                           | [CreativeWork](https://schema.org/CreativeWork) or [Event](https://schema.org/Event) | A CreativeWork or Event about this Thing. Inverse property: [about](https://schema.org/about). |
| `url`                                                 | [URL](https://schema.org/URL)                                | URL of the item.                                             |

As you can see, it contains almost any details you want. 

A similar method could be used to create a schema for Ishtar to provide good details for the artwork at question, it can be found under [Painting]( https://schema.org/Painting )



### Shema Example

One example from Ishtar Website can be:

```js
<script type="application/ld+json">
 {
   "@context":"http://schema.org",
   "@type":"VisualArtwork",
   "name":"Solitude on a Basalt Rock",
   "image":"Https://ishtar-art.de/ImageUploads/PaintingImages/2019-11-19_16-31-13/21_Nedal_Khweiss-5dd42660976b6.jpeg",
   "description":"A girl is sitting on the slopes of basalt mount at sunset.",
   "creator":[
      {
         "@type":"Person",
         "name":"Nedal Khweiss",
         "sameAs":"https://ishtar-art.de/artist/4"
      }
   ],
   "width":[
      {
         "@type":"Distance",
         "name":"80"
      }
   ],
   "height":[
      {
         "@type":"Distance",
         "name":"100"
      }
   ]
}
</script>
```

Which is the final result we are looking for in a finished project.



## Adding the Schemas to your site

After some search under this HUGE site, we found a good schemas that we can work for us, namely:

1. For the Cloths Store:
   1. ClothingStore (to define the client's physical store)
   2. Product (to define the stock the client has)
2. For Ishtar
   1. Painting
   2. Artist 



As Such we shall add The Cloths Shema to a WordPress Site the client has, as they use WooCommerce for their operations. 

And we shall add a Painting and Artist Schema to an Angular website.

This is not a development document, hence we shall mention a good candidate to apply JSON LD Schema to a website without actually implementing it, which shall be in a separate Blog.

### WordPress

we simply can add a plugin called Markup (JSON-LD) and config it.

### Angular

We used `@ngx-lite/json-ld` for our projects, but it is not hard to implement it in the project using standard practices.



## Final Remarks

If there is one thing you want to take from this Blog, make it this points:

1. Schema.org is a place to standardize the products across all kind of websites.

2. Search for the schemas candidates before committing to one.
3. The Final Result should be validated using Google's [testing tools]( https://search.google.com/structured-data/testing-tool/u/0/ ), If on standard Angular you copy the snippet from your rendered script (using Chrome inspect from Dev Tools, or Firefox Dev Tools).
4. Always improve on your Schemas and provide more and more data into the schemas.





That's All folks!