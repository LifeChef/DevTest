# DevTest

## Developer Test: Backend Node.js and Frontend React

### Instructions:

1. You are tasked with building both a backend Node.js API server and a frontend React application. Follow the instructions carefully for each section.

2. **Time Limit:** You have up to 6hrs to complete both the backend and frontend sections. Please manage your time wisely.

3. **Scoring:** Your solution will be evaluated based on correctness, code quality, adherence to requirements, documentation, and additional features. Aim for a comprehensive and polished solution.

4. **Bonus Tasks:** There are optional bonus tasks at the end of each section. Completing them demonstrates your expertise and may earn you extra points.

### Section 1: Backend Node.js

#### API Server

1. **Create an API Server:** Set up an API server using [Express](https://expressjs.com/) and TypeScript. Implement a GET endpoint “/hello” that responds with a JSON object containing the key “alive” and the server time as the value.

2. **Entity Schema:** Define an entity schema for the “Review” model following the provided TypeScript interface.

```js
  interface Review {
  id: number;
  text1: string;
  text2: string;
  text3: string;
  summary: string;
  nickname: string;
  createdAt: string; // DateTime ISO string, when model created
  updatedAt: string; // DateTime ISO string, when model updated
  }
```

You have two options:

   a) **Option A:** Add [Prisma](https://www.prisma.io/) and create a schema for PostgreSQL using the “Review” model.

   b) **Option B:** Implement in-memory storage as a fallback.

4. **CRUD REST Endpoints:** Create CRUD REST endpoints for the “Review” model. Ensure that the “list” endpoint supports pagination options (take: number, skip: number) and sort options (orderBy: {“field”: “asc|desc”}).

5. **Database Integration:** Connect the CRUD endpoints to the database.

6. **Data Population:** Populate the database with approximately 100 randomly generated records for the “Review” model.

#### Print Service

1. **Create a Print Service:** Develop a “print” service using Express and TypeScript.

2. **Add a POST Endpoint:** Implement a POST endpoint “/print.” The input body should contain the “Review” model. Respond with a status 200 and JSON {“status”: “ok”}.

3. **Data Storage:** Save the input request body from “/print” as a JSON file in the “restinput” folder. Name it `review${Date.now()}.json`.

#### API and Print Service Integrations

1. **Integration Configuration:** On the API server, add an environment variable named “integration_transport” with possible values: “rest” and “sqs”.

2. **Message Queue Setup:** Set up a local SQS-compatible message queue system using [ElasticMQ](https://github.com/softwaremill/elasticmq) with Docker or as a stand-alone application. Create the necessary queue.

3. **SQS Consumer:** In the Print service, add an SQS consumer using [sqs-consumer](https://www.npmjs.com/package/sqs-consumer) and attach it to the created queue. Save all input messages from the queue in the “sqsinput” folder with the name `review${Date.now()}.json`.

4. **Integration Handling (REST):** On the API server, when “integration_transport” is set to “rest,” create and update endpoints to save data to the database. Send the Review model to the Print service with a POST request to the “/print” endpoint.

5. **Integration Handling (SQS):** On the API server, when “integration_transport” is set to “sqs,” save the data to the database and send the Review model to the Print service using [sqs-producer](https://www.npmjs.com/package/sqs-producer) to the created queue.

6. **Bonus Tasks (Optional):** Implement error handling, unit tests, and documentation for your backend code. Bonus points for security measures like input validation and authentication.

### Section 2: Frontend React

#### Frontend Application

1. **Create a Next.js Application:** Set up a [Next.js](https://nextjs.org/) application with TypeScript and integrate [Tailwind CSS](https://tailwindcss.com/).

2. **Pages:** Create two pages: “list” and “details.” The “details” page should support the GET parameter `{id}`.

3. **API Integration:** Connect your frontend application to the API server using environment variables.

#### List Page

1. **List Page Layout:** On the “list” page, create a layout with the following elements:

   - “Create” link at the top right that opens the “details” page.
   - Request reviews from the API server to display the first 10 records.
   - “Load more” button at the bottom to load the next 10 records.
   - Render a list of review records between “Create” and “Load more” elements. Each record should display: id, createdAt, updatedAt, and a “delete” button.
   - Implement date formatting for createdAt and updatedAt as “Fri Nov 29, 2023.”

2. **Delete Review:** Implement functionality to delete a review from the database when the “delete” button is clicked. Update the list after a successful deletion.

3. **Details Page:** Clicking on a review entry should open the “details?id={id}” page and fill out the form with data from the API server.

#### Details Page

1. **Page Layout:** Design the “details” page layout based on the provided [Figma design](https://www.figma.com/file/UwMW3Ix6tFoGtMcwNoTE8O/Review?node-id=0%3A1). Use Tailwind CSS for styling and [React Hook Form](https://react-hook-form.com/) for processing forms. Note that the rating and stars are static elements.

2. **Form Submission:** Implement form submission for input fields. When submitting, use the create “api” endpoint for a new review or the update endpoint for existing reviews.

3. **Bonus Tasks (Optional):** Implement state management, authentication, client-side routing, and responsive design in your frontend application. Bonus points for performance optimizations and accessibility features.

### Section 3: Submission

1. **Submission:** Package your entire solution, including backend and frontend code, into a compressed file (e.g., ZIP). Include any necessary documentation or instructions for running your application.

2. **Code Review:** After submitting, your solution will be reviewed for correctness and quality. Feedback will be provided based on your code and its execution.

3. **Interview (Optional):** You may be contacted for an interview to discuss your solution, explain your design choices, and answer any questions.

Good luck and we are looking forward seing your work!
