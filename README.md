# zv-mongo-query-handler
Provides filtering, sorting, projecting, and paginating with MongoDB, through the Mongoose driver, using query string parameters.

### Basic Usage
```
const QueryHandler = require( 'zv-mongo-query-handler' );

// inside GET ALL endpoint controller
const queryHandler = new QueryHandler(User.find(), req.query)
                            .filter()
                            .sort()
                            .project()
                            .paginate();
const users = await queryHandler.query;
```
Required arguments are the *mongoose* ***query***, e.g. *User.find()*, and the ***req.query*** object. Chaining of all the available methods are not mandatory.

## Methods
**filter()**
- handles *gt*, *gte*, *lt*, and *lte* parameters: e.g.: `/api/v1/users?difficulty=easy&duration[gte]=5&price[lt]=1500`

**sort()**
- handles sorting e.g.: `/api/v1/users?sort=-price,duration`

**project()**
- handles limiting of selected fields e.g.: `/api/v1/users?fields=name,duration,ratingsAverage,price`

**paginate()**
- handles pagination e.g. `/api/v1/users?page=2&limit=10`
- *limit* parameter is optional - defaults to 100