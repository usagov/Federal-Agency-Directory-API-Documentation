# Federal Agency Directory API Documentation

## On This Page

*   [About the API](#about-the-api)
*   [Changes to the API](changes-to-the-api)
*   [About the Data](#about-the-data)
*   [Accessing the API](#accessing-the-api)
*   [API Methods](#api-methods)
*   [API Methods That Return Agency Records in a Tree Form](#api-methods-that-return-agency-records-in-a-tree-form)
*   [Terms of Service](#terms-of-service)

## About the API

We make the content you see in our [directory of federal agencies](/directory/federal/index.shtml) available in both English and Spanish via a REST API. The API programmatically returns all of the information contained in the directory, or you can query the API to return just a subset of the available information.

If you are using the Federal Agency Directory API and have questions, feedback, or want to tell us about your product, please [e-mail us](mailto:usagov-developers@gsa.gov).

## Changes to the API

On December 28, 2012, we launched version 2.0 of the API and made the following changes:

*   Launched new methods to return directory records in a hierarchical fashion.
*   Results can now be returned using XML and JSONP, as well as straight JSON.
*   The Interface method was removed.

On January 28, 2014, we launched version 2.1 of the API and made the following additions to the data model:

*   Added the CFO_Agency field.
*   Added the Inventory_URL field.
*   Added the Fed_Branch field.

## About the Data

The data in the Federal Agency Directory API is based on the [English](/directory/federal/index.shtml) and [Spanish](/gobiernousa/directorios/federal/index.shtml) federal agency directories. We gather this data from the agency information listed in the [U.S. Government Manual](http://www.usgovernmentmanual.gov), and independent research by our staff.

There is no schedule for data updates; we update data continually, and as needed. Early versions of the API may have incomplete and inconsistent data. We are working to continually develop the data in our directory records.

If you have suggestions about what types of data you would like to see in the Federal Agency Directory API, please [e-mail us](mailto:usagov-developers@gsa.gov).

### About the Spanish Data

GobiernoUSA.gov and the North American Academy of the Spanish Language (ANLE, per its Spanish acronym) worked together to review federal agencies Spanish translations to ensure language accuracy and consistency throughout the government. ANLE, the highest authority on Spanish language in the United States, and GobiernoUSA.gov have the joined mission of improving and standardizing the use of Spanish language in government communications.

This collaboration, possible through a signed agreement between the two institutions, resulted in a list of **official** Spanish language translations of federal agencies, available through this API.

## Accessing the API

Our Federal Agency Directory API is accessible via HTTP GET requests and does not require a login or API key to use.

The base URL for the API is http://www.usa.gov/api/USAGovAPI/contacts.{format}/. Append the API call you’d like to make to this URL.

Currently, three output formats are available:

1.  JSON (such as http://www.usa.gov/api/USAGovAPI/contacts.json/contacts)
2.  XML (such as http://www.usa.gov/api/USAGovAPI/contacts.xml/contacts)
3.  JSONP (such as http://www.usa.gov/api/USAGovAPI/contacts.jsonp/contacts?callback=callmemaybe). When requesting JSONP, you should include a callback parameter with the name of the callback function you would like called.

For the purposes of this documentation, only JSON sample calls and results will be shown.

### API Result Formats

The Federal Agency Directory API returns results in json, with an optional callback parameter to enable jsonp support.

### Interactive Documentation for the API

If you're interested in trying out the Federal Agency Directory API, we have an [interactive test page](http://www.usa.gov/About/developer-resources/federal-agency-directory/interactivedoc.shtml#!/contacts). On this page, you can try different parameters and see the results.

### API Data Model

The following fields are associated with directory records. Please note that not every record has data in every field, and the API will only return completed fields.

*   **Id** - A unique identifier for each directory record
*   **Name** – The name of the agency.
*   **Fed_Branch** - The branch of government the agency belongs too. The possible values are EXEC for the executive branch, LEG for the legislative branch, or JUD for the judicial branch.
*   **Description** – A brief description of the agency.
*   **CFO_Agency** - Wether the agency was required to create a Chief Financial Officer position in accordance with the [Chief Financial Officers Act of 1990](http://thomas.loc.gov/cgi-bin/query/z?c101:H.R.5687.enr:).
*   **Language** – Whether the record is in English or Spanish.
*   **Subdivision** – Used for mailing items to the agency.
*   **Street1** – A first line of address information (such as the street address) for the agency’s main office.
*   **Street2** – A second line of address information for the agency’s main office.
*   **City** – The city of the agency’s main office.
*   **StateTer** – The state of the agency’s main office.
*   **Zip** – The postal zip code of the agency’s main office.
*   **Email** – The e-mail address for the agency’s main office.
*   **Phone** – The phone number of the agency’s main office (may contain more than one).
*   **TTY** – The TTY number of the agency’s main office (may contain more than one).
*   **Tollfree** – The toll-free number to contact the agency (may contain more than one).
*   **SMS** – Any services offered via text messaging by the agency.
*   **Synonym** – Alternative names used commonly to refer to the agency (may contain more than one).
*   **URI** – The URL to access the agency’s complete directory record via the API.
*   **Source_Url** – The USA.gov or GobiernoUSA.gov URL that contains the record.
*   **Inventory_URL** - The URL to access the agency's program inventory on [Performance.gov](http://www.performance.gov/).

**URLs**

The directory API returns several types of URLs that can be used to link to the agency.

*   **Web_Url** – Main URLs for the agency (may contain more than one).
*   **Contact_Url** – URLs for the public to contact the agency (may contain more than one).
*   **In_Person_Url** – URLs for the public to find out how to interact with the agney in person (may contain more than one).
*   **Form_Url** – URLs for the agency to find forms from the agency (may contain more than one).

For each of these URLs, the following sub-data elements are returned:

*   **Url** – The URL to the web page.
*   **Description** – A description of the URL.
*   **Language** – Whether the web page located at the URL is in English (en) or Spanish (es).

**Agency Relationships**

Additionally, the directory API returns information on the hierarchical relationship between federal agencies.

*   **Parent** – The parent of the agency. such as the Department of the Treasury for the Internal Revenue Service.
*   **Child** – Any children departments or agencies for the agency. such as the Census Bureau for the Department of Commerce (may contain more than one of these).
*   **Alt_Language** – The record for the agency in Spanish, if the record is in English, and vice versa.

For each of these relationships, the following sub-data elements are returned for the related agency:

*   **Id** – A unique identifier for each directory record
*   **Name** – The name of the agency.
*   **URI** – The URL to access the agency’s complete directory record via the API.
*   **For Alt_Language only, Language** – Whether the alternate language record is in English (en) or Spanish (es).

## API Methods

As of version 2.0, the methods of the Federal Agency Directory API are broken down into two categories. The first category simply returns a list of agency records. The second category returns a hierarchical structure of the agency records, making it easy to form a tree. The tree can show that the [Food and Drug Administration](http://www.usa.gov/directory/federal/food-and-drug-administration.shtml) is part of the [Department of Health and Human Services](http://www.usa.gov/directory/federal/department-of-health-and-human-services.shtml). This is just one example.

### API Methods That Return A List of Agency Records

### Contacts

Contacts is a general purpose call that, by default, will return all of the agency directory records. However, you can pass parameters into contacts that allow you to filter the records returned by the API in powerful ways.

**Parameters**

**query_filter** – Return only agency directory records that meet the criteria you enter into this parameter. In general, the filter takes the form of {field_name}::{value}[|{field_name}::{value}]*. Additionally, for names, you can perform substring searches by surrounding {value} with asterixis.

For example, if you want to return all agencies that have the word “commission” in their title, you can use a query_filter of name::_commission_. Likewise, if you want to find all commissions who have their main address in Virginia, you can use a query_filter of: name::_commission_|state::VA

See the data model above for a list of field names that you can query on.

**result_filter_** _– Return only the fields listed here (separated by |) as opposed to every field in each directory record. For example, use a result_filter of name|phone to return only names and phone numbers.

See the data model above for a list of field names that you can specify be returned.

**sort** – Allows you to specify the sort order of the returned agency directory records. For example, use a sort of name to sort the results by the agency’s name. You can also cause the sort to go in descending order by prepending the field name with a -, such as -name.

See the data model above for a list of field names that you can sort the results on.

### /contacts/tree/independent

The independent method will return every agency record that has no parent and no child, such as the [National Railroad Passenger Corporation](http://www.usa.gov/directory/federal/amtrak.shtml).

### /contacts/tree

The tree method returns every agency record, and, optionally, includes sub-agencies as part of their parent agency’s record.

**Paramaters**

**include_descendants** - Set to true if you want the API to return the descendants directly as part of their parent agency’s record.

### /contacts/tree/dependent

The dependent method returns every agency record that has sub-agencies, and, optionally, includes sub-agencies as part of their parent agency’s record.

**Parameters**

**include_descendants** - Set to true if you want the API to return the descendents directly as part of their parent agency’s record.

### /contact/{identifier}/tree/sibling

The sibling method will return all of the agency records that are siblings to the agency represented by the id specified in the REST URL. It will also return the record for the id specified as well.  

The only difference between the result format of the sibling method and the more generic contacts method is that the siblings method does not return the child and parent data elements as part of it’s results.

For example, if you request the sibling agencies for the [U.S. Botanic Garden](http://www.usa.gov/directory/federal/botanic-garden.shtml) (id 49108), the API will return records for both the U.S. Botanic Garden and the [U.S. Capitol Visitor Center](http://www.usa.gov/directory/federal/us-capitol-visitor-center.shtml), as both of these agencies are part of the [Architect of the Capitol](http://www.usa.gov/directory/federal/architect-of-the-capitol.shtml).

If you desired the results in JSON format, the API call for this query would look like the following:
 http://www.usa.gov/api/USAGovAPI/contacts.json/contact/49108/tree/sibling

### Sample Results For These Methods

For API methods that return a list of directory records, the API will return an array of objects, such as:

The API will return an array of objects, such as:

```
{
   "Contact":[
      {
         "Id":"52663",
         "URI":"http://www.usa.gov/api/USAGovAPI/contacts.json/contact/52663",
         "Language":"en",
         "Name":"U.S. Access Board",
         "Source_Url":"http://www.usa.gov/directory/federal/us-access-board.shtml",
         "Street1":"1331 F Street, NW",
         "Street2":"Suite 1000",
         "City":"Washington",
         "StateTer":"DC",
         "Zip":"20004-1111",
         "Synonym":[
            "Access Board"
         ],
         "Phone":[
            "202-272-0080"
         ],
         "Tollfree":[
            "800-872-2253"
         ],
         "TTY":[
            "202-272-0082",
            "800-993-2822"
         ],
         "Email":"info@access-board.gov",
         "Contact_Url":[
            {
               "Url":"http://www.access-board.gov/contact.htm",
               "Description":"Contact the U.S. Access Board ",
               "Language":"en"
            },
            {
               "Url":"http://www.access-board.gov/contact.htm#email",
               "Description":"E-mail Directory",
               "Language":"en"
            },
            {
               "Url":"http://www.access-board.gov/contact.htm#Phone",
               "Description":"Phone Directory",
               "Language":"en"
            },
            {
               "Url":"http://www.access-board.gov/enforcement/filing.htm",
               "Description":"File an Accessibility Complaint",
               "Language":"en"
            }
         ],
         "Web_Url":[
            {
               "Url":"http://www.access-board.gov/",
               "Description":"U.S. Access Board ",
               "Language":"en"
            }
         ],
         "In_Person_Url":[
            {
               "Url":"http://www.access-board.gov/contact.htm#Location",
               "Description":"Map and Directions",
               "Language":"en"
            }
         ],
         "Description":"The Access Board is an independent federal agency devoted to accessibility for people with disabilities. The Board develops and maintains design criteria for the built environment, transit vehicles, telecommunications equipment, and for electronic and information technology. ",
         "Alt_Language":[
            {
               "Id":"50175",
               "URI":"http://www.usa.gov/api/USAGovAPI/contacts.json/contact/50175",
               "Name":"Consejo de Acceso de Estados Unidos",
               "Language":"es"
            }
         ]
      },
      {
         "Id":"61787",
         "URI":"http://www.usa.gov/api/USAGovAPI/contacts.json/contact/61787",
         "Language":"en",
         "Name":"Medicaid and CHIP Payment and Access Commission",
         "Source_Url":"http://www.usa.gov/directory/federal/medicaid-chip-payment-access-commission.shtml",
         "Street1":"1800 M Street, NW",
         "Street2":"Suite 350N",
         "City":"Washington",
         "StateTer":"DC",
         "Zip":"20036",
         "Phone":[
            "202-273-2460"
         ],
         "Email":"webmaster@macpac.gov",
         "Web_Url":[
            {
               "Url":"http://www.macpac.gov",
               "Description":"Medicaid and CHIP Payment and Access Commission ",
               "Language":"en"
            }
         ]
      }
   ]
}

```

If you set include_descendents to true in the tree or descendants methods, parent agencies will include an array called "Contact" with their child agency records, such as in this snippet:

```
{
   "Contact":[
      {
         "Id":"49015",
         "URI":"http://www.usa.gov/api/USAGovAPI/contacts.json/contact/49015",
         "Language":"en",
         "Name":"U.S. Department of Agriculture (USDA)",
         "Source_Url":"http://www.usa.gov/directory/federal/department-of-agriculture.shtml",
         "Street1":"1400 Independence Ave., S.W.",
         "City":"Washington",
         "StateTer":"DC",
         "Zip":"20250",
         "Synonym":[
            "Agriculture Department",
            "Department of Agriculture"
         ],
         "Phone":[
            "202-720-2791"
         ],
         "Contact_Url":[
            {
               "Url":"http://usda.gov/wps/portal/usda/usdahome?navid=CONTACT_US",
               "Description":"Contact the U.S. Department of Agriculture (USDA) ",
               "Language":"en"
            },
            {
               "Url":"http://www.fns.usda.gov/cnd/Contacts/StateDirectory.htm",
               "Description":"Child Nutrition Programs",
               "Language":"en"
            },
            {
               "Url":"http://www.fns.usda.gov/snap/contact_info/default.htm",
               "Description":"Food Stamps",
               "Language":"en"
            },
            {
               "Url":"http://www.fsis.usda.gov/Food_Safety_Education/USDA_Meat_&_Poultry_Hotline/index.asp",
               "Description":"Meat and Poultry Hotline",
               "Language":"en"
            },
            {
               "Url":"http://offices.sc.egov.usda.gov/employeeDirectory/app",
               "Description":"Employee Directory",
               "Language":"en"
            }
         ],
         "Web_Url":[
            {
               "Url":"http://www.usda.gov/wps/portal/usda/usdahome",
               "Description":"U.S. Department of Agriculture (USDA) ",
               "Language":"en"
            }
         ],
         "In_Person_Url":[
            {
               "Url":"http://www.rurdev.usda.gov/recd_map.html",
               "Description":"Rural Development Office Locator",
               "Language":"en"
            },
            {
               "Url":"http://apps.ams.usda.gov/FarmersMarkets/",
               "Description":"Farmers Markets Near You",
               "Language":"en"
            },
            {
               "Url":"http://offices.sc.egov.usda.gov/locator/app",
               "Description":"Find a Service Center Near You",
               "Language":"en"
            }
         ],
         "Description":"The Department of Agriculture provides leadership on food, agriculture, natural resources, and related issues.",
         "Alt_Language":[
            {
               "Id":"50072",
               "URI":"http://www.usa.gov/api/USAGovAPI/contacts.json/contact/50072",
               "Name":"Departamento de Agricultura",
               "Language":"es"
            }
         ],
         "Contact":[
            {
               "Id":"48012",
               "URI":"http://www.usa.gov/api/USAGovAPI/contacts.json/contact/48012",
               "Language":"en",
               "Name":"Center for Nutrition Policy and Promotion (CNPP)",
               "Source_Url":"http://www.usa.gov/directory/federal/center-for-nutrition-policy-and-promotion.shtml",
               "Street1":"3101 Park Center Dr., 10th Floor",
               "City":"Alexandria",
               "StateTer":"VA",
               "Zip":"22302-1594",
               "Phone":[
                  "703-305-7600"
               ],
               "Contact_Url":[
                  {
                     "Url":"http://www.cnpp.usda.gov/contacts.htm",
                     "Description":"Contact the Center for Nutrition Policy and Promotion (CNPP) ",
                     "Language":"en"
                  }
               ],
               "Web_Url":[
                  {
                     "Url":"http://www.cnpp.usda.gov/",
                     "Description":"Center for Nutrition Policy and Promotion (CNPP) ",
                     "Language":"en"
                  },
                  {
                     "Url":"http://www.choosemyplate.gov/",
                     "Description":"",
                     "Language":"en"
                  }
               ],
               "Description":"The USDA Center for Nutrition Policy and Promotion (CNPP) works to improve the health and well-being of Americans by developing and promoting dietary guidance that links scientific research to the nutrition needs of consumers."
            }
         ]
      }
   ]
}

```

For a complete list of fields returned in the json, see the data model description above. Please note that any field that contains more than one item in it (such as synonyms), is returned as an array and noted in the data model description.

We encourage you to try out the [interactive documentation](http://www.usa.gov/About/developer-resources/federal-agency-directory/interactivedoc.shtml#!/contacts) to learn more.

## API Methods That Return Agency Records in a Tree Form

These methods return agency records in a hierarchical data structure. In this way, you do not have to manually recreate the hierarchy yourself using the contacts method.

### /contact/{identifier}/tree/parent

The parent method returns the record of the parent agency specified in the REST URL and will continue up the agency hierarchy until the root agency is returned. Additionally, the record for the id specified will also be returned.

For example, if you request the parent tree for the Administration for Native Americans (agency id 49064) , the API will return a tree structure whose head is the U.S.  Department of Health and Human Services, with a child record for the Administration for Children and Families, which will then have a child record for the Administration of Native Americans.

With JSON-formatted results, this call would be made with this URL:  http://www.usa.gov/api/USAGovAPI/contacts.json/contact/49064/tree/parent

Likewise, if you request the parent tree for the Administration for Children and Families (agency id 47994), the API will return a tree structure whose head is the U.S. Department of Health and Human Services, with a child record for the Administration for Children and Families.  However, the structure will end at that point instead of continuing down the agency hierarchy.

With JSON-formatted results, this call would be made with this URL:  http://www.usa.gov/api/USAGovAPI/contacts.json/contact/47994/tree/parent

### /contact/{identifier}/tree/descendant

The descendant method will return a tree with the agency specified in the REST URL at it’s head. It will include all of the agency's sub-agencies as children. The tree will then continue in this fashion until the agencies with no children are returned.

For example, if you request the descendant tree of the Administration for Children and Families (agency id 47994), the API will return a tree structure with the record for the Administration for Children and Families at it’s head. There would then be child record for the Administration of Native Americans, since that agency is a subagency of the Administration for Children and Families.

With JSON-formatted results, this call would be made with this URL: http://www.usa.gov/api/USAGovAPI/contacts.json/contact/47994/tree/descendant

Likewise, if you request the descendant tree of the U.S. Department of Health and Human Services (agency id 49021), the API will return a tree structure with the U.S. Department of Health and Human Services record at it’s head, and have 15 child records for each of the sub-agencies.  The tree will continue in this manner until the entire U.S. Department of Health and Human Services hierarchy of agencies is exposed.

With JSON-formatted results, this call would be made with this URL: http://www.usa.gov/api/USAGovAPI/contacts.json/contact/49021/tree/descendant

### /contact/{identifier}/tree/branch

The branch method returns a tree that is the combination of the trees returned by the parent method and the descendant method for the id specified in the REST URL. With this one method, the API will return every parent and every descendant of a particular agency.

### /contact/{identifier}

The contact/{identifier} method will return the single directory record represented by the id specified in the REST URL. There are no children records returned when using this method.

### Sample Results For These Methods

For API methods that return a tree of directory records, the API will return an array of objects, such as:

```
{
  "Id": "49021",
  "URI": "http://www.usa.gov/api/USAGovAPI/contacts.json/contact/49021",
  "Language": "en",
  "Name": "U.S. Department of Health and Human Services (HHS)",
  "Source_Url": "http://www.usa.gov/directory/federal/department-of-health-and-human-services.shtml",
  "Street1": "200 Independence Avenue, S.W.",
  "City": "Washington",
  "StateTer": "DC",
  "Zip": "20201",
  "Synonym": [
    "Health and Human Services Department",
    "Department of Health and Human Services"
  ],
  "Contact_Url": [
    {
      "Url": "http://www.hhs.gov/contactus.html",
      "Description": "Contact the U.S. Department of Health and Human Services (HHS) ",
      "Language": "en"
    },
    {
      "Url": "http://www.acf.hhs.gov/acf_contact_us.html#state",
      "Description": "Child Support",
      "Language": "en"
    },
    {
      "Url": "http://www.acf.hhs.gov/programs/ofa/help",
      "Description": "Temporary Assistance for Needy Families (Welfare)",
      "Language": "en"
    },
    {
      "Url": "http://www.medicare.gov/ContactUs.asp",
      "Description": "Medicare",
      "Language": "en"
    },
    {
      "Url": "http://www.acf.hhs.gov/programs/ocs/liheap/about/contact_us.html",
      "Description": "Low Income Home Energy Assistance Program (LIHEAP)",
      "Language": "en"
    },
    {
      "Url": "https://cfo.gov/cfo-members/",
      "Description": "Employee Directory",
      "Language": "en"
    }
  ],
  "Web_Url": [
    {
      "Url": "http://www.hhs.gov/",
      "Description": "U.S. Department of Health and Human Services (HHS) ",
      "Language": "en"
    }
  ],
  "In_Person_Url": [
    {
      "Url": "http://eclkc.ohs.acf.hhs.gov/hslc/HeadStartOffices",
      "Description": "Head Start Program Locator",
      "Language": "en"
    }
  ],
  "Description": "The Department of Health and Human Services protects the health of all Americans and provides essential human services.",
  "Alt_Language": [
    {
      "Id": "50081",
      "URI": "http://www.usa.gov/api/USAGovAPI/contacts.json/contact/50081",
      "Name": "Departamento de Salud y Servicios Sociales – HHS",
      "Language": "es"
    }
  ],
  "Contact": [
    {
      "Id": "47994",
      "URI": "http://www.usa.gov/api/USAGovAPI/contacts.json/contact/47994",
      "Language": "en",
      "Name": "Administration for Children and Families (ACF)",
      "Source_Url": "http://www.usa.gov/directory/federal/administration-for-children--families.shtml",
      "Street1": "370 L'nfant Promenade, SW",
      "City": "Washington",
      "StateTer": "DC",
      "Zip": "20447",
      "Tollfree": [
        "1-888-289-8442 (Fraud Alert Hotline)"
      ],
      "Contact_Url": [
        {
          "Url": "http://www.acf.hhs.gov/programs/ana/about",
          "Description": "Contact the Administration for Children and Families (ACF) ",
          "Language": "en"
        },
        {
          "Url": "https://cfo.gov/cfo-members/",
          "Description": "Employee Directory",
          "Language": "en"
        },
        {
          "Url": "http://www.acf.hhs.gov/acf_contact_us.html#state",
          "Description": "Child Support",
          "Language": "en"
        },
        {
          "Url": "http://www.acf.hhs.gov/programs/ofa/help",
          "Description": "Temporary Assistance for Needy Families (Welfare)",
          "Language": "en"
        },
        {
          "Url": "http://www.childwelfare.gov/pubs/reslist/rl_dsp.cfm?rs_id=5&rate_chno=11-11172",
          "Description": "Report Child Abuse and Neglect",
          "Language": "en"
        },
        {
          "Url": "http://www.acf.hhs.gov/programs/ocs/liheap/about/contact_us.html",
          "Description": "Low Income Home Energy Assistance Program (LIHEAP)",
          "Language": "en"
        }
      ],
      "Web_Url": [
        {
          "Url": "http://www.acf.hhs.gov/",
          "Description": "Administration for Children and Families (ACF) ",
          "Language": "en"
        }
      ],
      "In_Person_Url": [
        {
          "Url": "http://eclkc.ohs.acf.hhs.gov/hslc/HeadStartOffices",
          "Description": "Head Start Program Locator",
          "Language": "en"
        },
        {
          "Url": "http://www.acf.hhs.gov/programs/cse/extinf.html",
          "Description": "Child Support Enforcement in Your State",
          "Language": "en"
        }
      ],
      "Description": "The ACF funds state, territory, local, and tribal organizations to provide family assistance (welfare), child support, child care, Head Start, child welfare, and other programs relating to children and families.",
      "Alt_Language": [
        {
          "Id": "50101",
          "URI": "http://www.usa.gov/api/USAGovAPI/contacts.json/contact/50101",
          "Name": "Administración de Asuntos de Niños y Familias",
          "Language": "es"
        }
      ],
      "Contact": [
        {
          "Id": "49064",
          "URI": "http://www.usa.gov/api/USAGovAPI/contacts.json/contact/49064",
          "Language": "en",
          "Name": "Administration for Native Americans",
          "Source_Url": "http://www.usa.gov/directory/federal/administration-for-native-americans.shtml",
          "Street1": "2nd Floor, West Aerospace Center",
          "Street2": "370 L'Enfant Promenade, SW",
          "City": "Washington",
          "StateTer": "DC",
          "Zip": "20447-0002",
          "Tollfree": [
            "877-922-9262"
          ],
          "Email": "anacomments@acf.hhs.gov",
          "Contact_Url": [
            {
              "Url": "http://www.acf.hhs.gov/programs/ana/about",
              "Description": "Contact the Administration for Native Americans ",
              "Language": "en"
            }
          ],
          "Web_Url": [
            {
              "Url": "http://www.acf.hhs.gov/programs/ana/",
              "Description": "Administration for Native Americans ",
              "Language": "en"
            }
          ],
          "Description": "The Administration for Native Americans promotes self-sufficiency and cultural preservation for Native Americans by providing social and economic development opportunities through financial assistance, training, and technical assistance.",
          "Alt_Language": [
            {
              "Id": "50125",
              "URI": "http://www.usa.gov/api/USAGovAPI/contacts.json/contact/50125",
              "Name": "Oficina de Asuntos Nativo Americanos",
              "Language": "es"
            }
          ]
        }
      ]
    }
  ]
}

```

## Terms of Service

By using this data, you agree to the [Terms of Service](/About/developer-resources/terms-of-service.shtml).