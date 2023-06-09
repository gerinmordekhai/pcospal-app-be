# PCOS Pal
Polycystic Ovary Syndrome (PCOS) is a collection of symptoms resulting from a disorder in the endocrine system and this condition is usually seen in reproductive-aged women. This syndrome may cause serious health problems. 
Women who experienced this syndrome may experience infertility, impaired glucose tolerance, depression, Obstructive Sleep Apnea (OSA), increased risk of endometrial cancer and liver disease, diabetes, weight problems, and also possible to give birth to premature babies. 
Many women, particularly in Indonesia, are unaware and they often ignore that they have symptoms or risk factors that increase their likelihood of experiencing PCOS. If not treated seriously, it’ll cause fatal consequences leading to death. 
Therefore, we want to develop an easy-to-use application to help detect possibilities if they are at risk of experiencing PCOS. Although PCOS cannot be completely cured, its symptoms can be controlled and managed with the right treatment and a healthy lifestyle. We chose this case because we want to help reduce the women's death rate from disease.

# Development Setup
This repository contains the backend RESTful API for the PCOS Pal application, which serves as the interface for performing Create, Read, Update, and Delete (CRUD) operations on the application's database. It also incorporates logic operations, including the calculation of Body Mass Index (BMI). By leveraging this API, the application can seamlessly interact with the database, enabling users to store, retrieve, update, and delete data related to PCOS Pal. Furthermore, the API's capability to compute BMI adds an essential feature to the application, allowing users to track their body weight and assess their health status. Overall, this repository plays a pivotal role in supporting the functionality and data management of the PCOS Pal application.

## Prerequisites
- NodeJS
- Node Package Manager (npm)
- MySQL
- Google Cloud Run
- Google Cloud Build
- Google Cloud SQL
- Chat GPT API Key

## Setting Up Project 
Please fork this repository first, then clone the repository that you have forked. You can clone your forked repository by using this following command:
```
git clone https://github.com/YOUR GITHUB USERNAME/pcospal-app-be.git
```

Then, open a terminal like bash, zsh, command prompt or powershell and install dependency with the following command:
```
npm install
```
this will install all dependencies which will be used.

This project uses [ExpressJS](https://expressjs.com/) as framework.

To support this application, we use several libraries such as:
- [Sequelize](https://sequelize.org/). Sequelize is a modern TypeScript and Node.js ORM for Oracle, Postgres, MySQL, MariaDB, SQLite and SQL Server, and more. Featuring solid transaction support, relations, eager and lazy loading, read replication and more.
- [JsonWebToken](https://www.npmjs.com/package/jsonwebtoken). JSON web token (JWT), is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.
- [openai](https://www.npmjs.com/package/openai). The OpenAI Node.js library provides convenient access to the OpenAI API from Node.js applications. Most of the code in this library is generated from our OpenAPI specification.

Next, edit the `app.yaml`.
Then, please change the database credentials in the `env_variables`:
```
env_variables: 
  DB_HOST: 
  DB_USER: 
  DB_PASSWORD: 
  DB_DATABASE: 
  DB_DIALECT: 
  DB_SOCKET: 

  APP_ENV: development
```

Next, you can retrieve your OpenAi API Key by following this instruction [OPENAI_API_KEY](https://tfthacker.medium.com/how-to-get-your-own-api-key-for-using-openai-chatgpt-in-obsidian-41b7dd71f8d3)

Finally, you can run the following command to run the API
```
npm run dev
```

This project will run on `https://localhost:8080`

### Setup Cloud Infrastructure
Since both Cloud SQL and Cloud Run are on the Google Cloud Platform, it’s better to connect by private IP for minimum network latency. Enable the “Private IP” option if it’s not enabled yet. Keep note of the network and private IP address which will be used later.

For now, you only need to understand that Serverless VPC Access allows Cloud Functions, Cloud Run services, and App Engine apps to access resources in a VPC network using their private IPs.

Compute Engine default service account by default, should have the Cloud SQL Client role with permissions to connect to Cloud SQL.

create a Cloud Run service and connect it to our Cloud SQL instance with the VPC connector just created.

for more detail please follow this instruction [CLOUD_SERVICES](https://towardsdatascience.com/how-to-connect-to-gcp-cloud-sql-instances-in-cloud-run-servies-1e60a908e8f2)


## Testing the API
You can try to hit the API using the POSTMAN application.

### API Endpoints
| METHOD | ENDPOINT | FUNCTION |
| ------ | -------- | -------- |
| [GET] | `/` | to see if the API works |
| [POST] | `/api/register` | register user account |
| [POST] | `/api/login` | login user account |
| [GET] | `/api/auth/user` | show user data |
| [POST] | `/api/auth/calculate-bmi` | calculate BMI |
| [POST] | `/api/auth/pcos` | create user answer (survey) |
| [POST] | `api/auth/pcos/result` | generate tips n trick with GPT |

### API Payloads
`/api/register`:
```json
{
    "firstName": " ",
    "lastName": " ",
    "phoneNumber": " ",
    "email": " ",
    "birthday": "YYYY-MM-DD",
    "password": " "
}
```

`/api/login`:
```json
{
    "email": " ",
    "password": " "
}
```

`/api/auth/calculate-bmi`:
```json
{
    "bodyWeight": 74,
    "bodyHeight": 180
}
```

`/api/auth/pcos`:
```json
{
    "age": 21,
    "bmi": 19.1,
    "pulseRate": 78,
    "cycle": "regular",
    "yearsOfMarriage": 7.0,
    "hip": 36,
    "waist": 30,
    "weightGain": "no",
    "hairGrowth": "no",
    "skinDarkening": "no",
    "hairLoss": "yes",
    "pimples": "no",
    "fastFood": "yes"
}
```