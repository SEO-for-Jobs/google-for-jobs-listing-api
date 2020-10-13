# google-for-jobs-listing-api (powered by SEO for Jobs)

SEO for Jobs APIs allow you to integrate Google for Jobs with ease and go beyond the basic job posting integration out of the box.

This API requires a valid SEO for Jobs accout. You can create a free account here: https://www.seo-for-jobs.com
Within your accout you can request an API token, which is also required for authentication.
The standard request limit is 50 requests per hour and can be increased on request.

## Basics

Root URL is ```https://app.seo-for-jobs.com/api/public```
API token must be present in ```x-api-token``` header.
Body Request type is ```application/json```

## API Calls

### ```GET /jobs```

Get a list of all job postings within your account.

**Parameters**

none

**Response (Example)**
````
{
  list: [
    {
      id: "2fd59d17-14ea-4b86-a3d8-c3126db5fbc6",
      title: "SAP S/4HANA Senior Developer",
      description: "Lorem ipsum dolor sit amet<br>consetetur …" 
      …
    },
    {…}
  ]
}
````

**CURL (Example)**
````
$curl -XGET -H 'x-api-key: cca265e6-5c40-4187-a0e9-713b4a9c453f' 'https://app.seo-for-jobs.com/api/public/jobs'
````

### ```POST /job```

Create a new job posting within your account.

**Parameters**

- ```status``` One of this "DRAFT" or "PUBLISHED"
- ```title``` String
- ```description``` HTML description (allowed tags: br, ul, li)
- ```employmentType``` NULL or list of this "INTERN", "PERDIEM", "FULLTIME", "PARTTIME", "TEMPORARY", "VOLUNTEER", "CONTRACTOR" (eg.: ["FULLTIME","PARTTIME"])
- ```salaryCurrency``` NULL or one of this "EUR", "CHF", "INR", "JPY", "USD"
- ```salaryValue``` Number (eg.: 42.00)
- ```salaryUnit``` NULL or one of this "DAY", "HOUR", "WEEK", "YEAR", "MONTH"
- ```streetAndNo``` String
- ```city``` String
- ```postalCode``` String (because of leading zeros)
- ```countryCode``` i18n country code (eg. "DE" or "FR").
- ```companyName``` String
- ```companyLogoUrl``` Full URL to a logo (250px x 250px, .png, .jpeg, .jpg)
- ```redirectUrl``` Full URL for redirecting after click on the "Apply Button" within Google for Jobs.

**Response (Example)**
````
{
  id: "2fd59d17-14ea-4b86-a3d8-c3126db5fbc6"
  status: "PUBLISHED",
  title: "SAP S/4HANA Senior Developer",
  description: "Lorem ipsum dolor sit amet<br>consetetur …" 
  …
}
````

**CURL (Example)**
````
$curl -XPOST -H 'x-api-key: cca265e6-5c40-4187-a0e9-713b4a9c453f' -H "Content-type: application/json" -d '{status: "PUBLISHED",title: "SAP S/4HANA Senior Developer",description: "Lore Ipsum …",employmentType: ["FULLTIME", "PARTTIME"],streetAndNo:"Jungfernstieg 47",city: "Hamburg",postalCode: "20354",countryCode: "DE",companyName: "SFJ",redirectUrl: "https://www.seo-for-jobs.de/jobs/sap-hana-senior-developer"}' 'https://app.seo-for-jobs.com/api/public/job'
````

### ```PUT /job/{id}```

Update an existing job posting with the corresponding {id}. Only submitted parameters will be updated. The update will be automatically pushed to Google in case the status is after the update process "PUBLISHED".

**Parameters**

- ```status``` One of this "DRAFT" or "PUBLISHED"
- ```title``` String
- ```description``` HTML description (allowed tags: br, ul, li)
- ```employmentType``` NULL or list of this "INTERN", "PERDIEM", "FULLTIME", "PARTTIME", "TEMPORARY", "VOLUNTEER", "CONTRACTOR" (eg.: ["FULLTIME","PARTTIME"])
- ```salaryCurrency``` NULL or one of this "EUR", "CHF", "INR", "JPY", "USD"
- ```salaryValue``` Number (eg.: 42.00)
- ```salaryUnit``` NULL or one of this "DAY", "HOUR", "WEEK", "YEAR", "MONTH"
- ```streetAndNo``` String
- ```city``` String
- ```postalCode``` String (because of leading zeros)
- ```countryCode``` i18n country code (eg. "DE" or "FR").
- ```companyName``` String
- ```companyLogoUrl``` Full URL to a logo (250px x 250px, .png, .jpeg, .jpg)
- ```redirectUrl``` Full URL for redirecting after click on the "Apply Button" within Google for Jobs.

**Response (Example)**
````
{
  id: "2fd59d17-14ea-4b86-a3d8-c3126db5fbc6"
  status: "PUBLISHED",
  title: "SAP S/4HANA Senior Developer",
  description: "Lorem ipsum dolor sit amet<br>consetetur …" 
  …
}
````

**CURL (Example)**
````
$curl -XPUT -H 'x-api-key: cca265e6-5c40-4187-a0e9-713b4a9c453f'  -H "Content-type: application/json" -d '{title: "SAP S/4HANA Junior Developer",employmentType: ["FULLTIME"]}' 'https://app.seo-for-jobs.com/api/public/job/2fd59d17-14ea-4b86-a3d8-c3126db5fbc6'
````

### ```DELETE /job/{id}```

Delete a job posting with the corresponding {id}.

**Parameters**

none

**Response (Example)**
````
{
  status: "SUCCESS"
} 
````

**CURL (Example)**
````
curl -XDELETE -H 'x-api-key: cca265e6-5c40-4187-a0e9-713b4a9c453f' 'https://app.seo-for-jobs.com/api/public/job/2fd59d17-14ea-4b86-a3d8-c3126db5fbc6'
````

## ```Errors```

In case an error occurred while processing your request you will get one of the following codes:

```API_TOKEN_INVALID```

The provided API Token was not found within an active account. An account is marked as "active" when it has an active package.

```REQUEST_LIMIT_REACHED```

The daily request limit is reached. your request limit will be reset within a sliding 24h window.

```UPGRADE_NECESSARY```

The total count of jobs with the status "PUBLISHED" has reached your package limit. Please upgrade your account to publish more jobs.

```ID_NOT_FOUND```

The provided ID for a specific job posting was not found.
