openapi: 3.0.1
info:
  title: Know Customer Plus (FCM API)
  description: |-
    KC+ is a risk-management solution that allows banks to standardize risk calculation process based on customer attributes. Risk assessments may be performed not only at the account opening process but also during the entire customer life cycle. KYC workflow builder uses configurable dynamic forms to enable tailored questions to each specific profile which are also available via API. More thorough and advanced than standard KYC (Know Your Customer) solutions it uses a comprehensive risk matrix including the status, range, and counts to calculate the risk based on customer’s attributes. The system offers the ability to add search criteria filters or create, amend or delete assessments. It uses advanced and fully configurable algorithms to calculate compliance risk scores of new and existing customers based on the customer profile. In this way, the system provides greater flexibility, accuracy, and control.
   
    **Note**: This API is for information purposes and cannot be used with the Standard Transact Developer Sandbox. The complete document is provided as part of a FCM release via the [FCM Team](https://www.temenos.com/contact-us/#contact).

    To learn more about Temenos FCM visit [temenos.com](https://www.temenos.com/products/financial-crime-mitigation/)
  version: v1.0.0
  "url": "api.server.com",
paths:
  /api/v1/computations/customer/calculateRisk:
    post:
      tags:
        - Customer Risk Computation
      summary: To compute the customer risk using risk matrix of customer's company
      description: 'To calculate the existing customer risk and will provide the risk calculate result as response <br />Note: if customer does not exist already then customer will be saved first to calculate the risk'
      operationId: calculateRisk
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/JsonCustomer'
        required: true
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/JsonRiskCalculationResult'
        '400':
          description: No risk matrix could not be found for that customer.
        '403':
          description: The authenticated user is not authorized to update a customer or to compute a risk
        '404':
          description: The mandatory data's are not found in the request
  /api/v1/computations/customer/onboard/computerisk:
    post:
      tags:
        - Customer Risk Computation
      summary: To onboard a customer and compute the risk using risk matrix
      description: 'To onboard a new customer then calculate risk of the newly onboarded customer and provide the risk details as a response <br />Note: if customer already exists in the database then customer details is updated before calculating the risk'
      operationId: onboardCustomerAndCalculateRisk
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/JsonCustomer'
        required: true
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/JsonRiskCalculationResult'
        '400':
          description: No risk matrix could not be found for that customer.
        '403':
          description: The authenticated user is not authorized to update a customer or to compute a risk
        '404':
          description: The required data's are not found in the request or in the database
  '/api/v1/resource/customer/json/schema/{id}':
    get:
      tags:
        - Customer Schema Information
      summary: Get the schema for the customer
      description: 'Retrieve schema for the customer based on id provided '
      operationId: get
      parameters:
        - name: id
          in: path
          description: 'The version number of the schema to retrieve.Latest version: 2.0'
          required: true
          schema:
            type: string
          example: V2
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                type: string
        '404':
          description: No customer Found.
  '/api/v1/resource/customer/dynamic-field-definitions/list/{company}':
    get:
      tags:
        - CIF Field Definitions
      description: Fetches the list of CIF Field Definitions and returns the definition list.
      operationId: listCifFieldDefinitions
      parameters:
        - name: company
          in: path
          description: Name of the Company
          required: true
          schema:
            type: string
          example: GB0010001
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/JsonCifFieldDefinitionResponse'
        '400':
          description: No CIF Field definition found for that customer.
        '403':
          description: The authenticated user is not authorized to fetch CIF Field definitions
  '/api/v1/resource/customer/assessments/list/{company}':
    get:
      tags:
        - Risk Assessments
      summary: Get the List of Assessments
      description: Lists all the assesments based on the company provided.
      operationId: listAssessments
      parameters:
        - name: company
          in: path
          description: Name of the company
          required: true
          schema:
            type: string
          example: GB0010001
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/JsonAssessmentResponse'
        '401':
          description: The authenticated user is not authorized to view the risk assessments
  '/api/v1/resource/customer/sectors/list/{company}':
    get:
      tags:
        - Sectors
      summary: Get the Sectors for provided company
      description: Provides list of sector information for the provided company.
      operationId: listSectors
      parameters:
        - name: company
          in: path
          description: The company that the Sectors belongs to
          required: true
          schema:
            type: string
          example: GB0010001
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonSectors'
        '403':
          description: The authenticated user is not authorized.
  /api/v1/computations/customer/form/submit:
    post:
      tags:
        - Customer Form Submission
      summary: To submit answers of the form for a customer
      description: 'To submits customers answers of a form, returns the computed risk after customer details updated with form''s answers. Onboarding as well as Enhance Due Diligence form submission can be made via this service.<br/>Note : Form should be already available and in active state'
      operationId: formSubmit
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/FormSubmit'
        required: true
      responses:
        '200':
          description: API success response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/JsonRiskCalculationResult'
        '400':
          description: The request format/data is invalid
        '403':
          description: The authenticated user is not authorized to update a customer or to compute a risk
        '404':
          description: No such form exists.
  /api/v1/resource/customer/information/list:
    get:
      tags:
        - Customer Information
      summary: Get the Customer Information
      description: Provides information on the provided customer and company. The choice of what information to provide is controlled through the infoType parameter.
      operationId: getDetails
      parameters:
        - name: customerId
          in: query
          description: The id of the Customer
          required: true
          schema:
            type: string
          example: 190056
        - name: company
          in: query
          description: The company that the Customer belongs to
          required: true
          schema:
            type: string
          example: GB0010001
        - name: infoType
          in: query
          description: 'An list of Customer information types. Possible values are: ALL, GENERAL_INFO, DYNAMIC_FIELDS, RISK_CALCULATIONS, HISTORICAL_ALERTS, LIVE_ALERTS.'
          required: false
          schema:
            type: array
            items:
              type: string
              enum:
                - ALL
                - GENERAL_INFO
                - DYNAMIC_FIELDS
                - RISK_CALCULATIONS
                - HISTORICAL_ALERTS
                - LIVE_ALERTS
          example: 'GENERAL_INFO,DYNAMIC_FIELDS'
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                type: object
        '404':
          description: Customer with the provided id cannot be found for the company
  '/api/v1/customer/{customerId}/documents/status':
    put:
      tags:
        - Customer Update
      summary: To Update Customer
      description: 'Update the customer details on the provided customerId. '
      operationId: updateCustomer
      parameters:
        - name: customerId
          in: path
          description: The id of the Customer
          required: true
          schema:
            type: string
          example: 190078
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/JsonCustomer'
        required: true
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/CustomerUpdateSuccessResponse'
        '400':
          description: 'Request json format is invalid '
        '403':
          description: 'The authenticated user is not authorized to update a customer '
        '404':
          description: 'Customer not found for customerId '
        '500':
          description: Something doesn't go well while communicating with the server.
  '/api/v1/customers/form_submission/{formSubmissionId}/properties':
    get:
      tags:
        - Form Status Update
      operationId: getFormSubmissionProperty
      parameters:
        - name: formSubmissionId
          in: path
          required: true
          schema:
            type: integer
            format: int32
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                type: object
                additionalProperties:
                  type: object
  '/api/v1/customers/{customerId}/forms/{formId}/documents/status':
    put:
      tags:
        - Form Status Update
      summary: To Update Form Status
      description: 'Update the Form Status on the provided customerId and formId. '
      operationId: updateFormStatus
      parameters:
        - name: customerId
          in: path
          description: The id of the Customer
          required: true
          schema:
            type: string
          example: 190079
        - name: formId
          in: path
          description: The id of the form
          required: true
          schema:
            type: string
          example: Form_001
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/FormStatusRequest'
        required: true
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/FormUpdateSuccessResponse'
        '400':
          description: 'Request json format is invalid '
        '404':
          description: 'Customer not found for customerId, Form is invalid or Form Status is invalid '
        '500':
          description: Something doesn't go well while communicating with the server.
  '/api/v1/customers/{customerId}/forms/{formReference}/properties':
    put:
      tags:
        - Form Status Update
      operationId: updateFormStatusByFormReference
      parameters:
        - name: customerId
          in: path
          required: true
          schema:
            type: string
        - name: formReference
          in: path
          required: true
          schema:
            type: string
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/FormUpdateRequest'
        required: true
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/FormSubmissionUpdateResponse'
  '/api/v1/customers/form_submissions/{formSubmissionId}/properties':
    put:
      tags:
        - Form Status Update
      operationId: updateFormStatusByFormSubmissionId
      parameters:
        - name: formSubmissionId
          in: path
          required: true
          schema:
            type: integer
            format: int32
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/FormUpdateRequest'
        required: true
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/FormSubmissionUpdateResponse'
  '/api/v1/resource/customer/{customerId}/status':
    get:
      tags:
        - Customer Watchlist Link Status
      summary: Get watchlist link status of a customer.
      description: 'To get customer watchlist link status of a customer by using customerId. Possible statuses are IsInWatchlist, HasBeen, Internal & SelfDeclared (The statuses are configurable in dynamic fields). Except SelfDeclared other statuses holds the details of watchlist name, linked date, review date, alert reference, entry reference. SelfDeclared status holds a plain text of declaration from customer.'
      operationId: getStatus
      parameters:
        - name: customerId
          in: path
          description: The id of the Customer.
          required: true
          schema:
            type: string
          example: 12345
        - name: listName
          in: query
          description: Watchlist name.
          required: false
          schema:
            type: string
          example: OFAC
      responses:
        '200':
          description: Successful Response
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonCustomerStatusesResponse'
        '400':
          description: Bad request. Request parameters not valid.
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonErrorResponse'
        '403':
          description: Not authorized to access this API.
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonErrorResponse'
    post:
      tags:
        - Customer Watchlist Link Status
      summary: Add watchlist link status to a customer
      description: To add a new watch list status for a customer.
      operationId: saveDetails
      parameters:
        - name: customerId
          in: path
          description: The id of the Customer.
          required: true
          schema:
            type: string
          example: 12345
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/JsonCustomerStatus'
        required: true
      responses:
        '200':
          description: Successful Response
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonCustomerStatusesResponse'
        '400':
          description: Bad request. Request parameters not valid.
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonErrorResponse'
        '403':
          description: Not authorized to access this API.
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonErrorResponse'
    delete:
      tags:
        - Customer Watchlist Link Status
      summary: Deletes a customer watchlist link status
      description: To delete a customer watchlist link status by using customerId
      operationId: deleteStatus
      parameters:
        - name: customerId
          in: path
          description: The id of the Customer.
          required: true
          schema:
            type: string
          example: 12345
        - name: listName
          in: query
          description: Watchlist name.
          required: true
          schema:
            type: string
          example: OFAC
        - name: status
          in: query
          description: Name of the link status.
          required: true
          schema:
            type: string
          example: IsInWatchList
      responses:
        '200':
          description: Successful Response
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonResponse'
        '400':
          description: Bad request. Request parameters not valid.
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonErrorResponse'
        '403':
          description: Not authorized to access this API.
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonErrorResponse'
  '/api/v1/resource/customer/{customerId}/periodic_review':
    post:
      tags:
        - Customer Watchlist Link Status
      summary: Create review request for customer watchlist link status
      description: 'To create review request for customer watchlist link status. The link status can be validated by reviewing this request and can be updated. For example, customer can exists in watchlist today but that can change over a time which requires a review and update to link status.'
      operationId: createPeriodicReview
      parameters:
        - name: customerId
          in: path
          description: The id of the Customer.
          required: true
          schema:
            type: string
          example: 12345
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/JsonCustomerStatus'
        required: true
      responses:
        '200':
          description: Successful Response
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonCustomerStatusesResponse'
        '400':
          description: Bad request. Request parameters not valid.
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonErrorResponse'
        '403':
          description: Not authorized to access this API.
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonErrorResponse'
  '/api/v1/resource/customer/{customerId}/nextreview':
    get:
      tags:
        - Customer Watchlist Link Status
      summary: Get next review date of a watchlist link status
      description: To get next review date of a watchlist link status of a customer by using customerId
      operationId: getNextReview
      parameters:
        - name: customerId
          in: path
          description: The id of the Customer.
          required: true
          schema:
            type: string
          example: 12345
        - name: listName
          in: query
          description: Watchlist name.
          required: true
          schema:
            type: string
          example: OFAC
        - name: status
          in: query
          description: Name of the link status.
          required: true
          schema:
            type: string
          example: IsInWatchList
      responses:
        '200':
          description: Successful Response
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonCustomerStatusesResponse'
        '400':
          description: Bad request. Request parameters not valid.
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonErrorResponse'
        '403':
          description: Not authorized to access this API.
          content:
            '*/*':
              schema:
                $ref: '#/components/schemas/JsonErrorResponse'
  /api/v1/resource/framework/forms/submitted:
    get:
      tags:
        - Form Information
      summary: Get the Form Information by customerId
      description: Retrieve a form information by using customerId
      operationId: getSubmittedForms
      parameters:
        - name: customerId
          in: query
          description: The id of the Customer
          required: true
          schema:
            type: string
        - name: formReference
          in: query
          description: The formReference that belongs to Customer
          required: false
          schema:
            type: string
        - name: lastSubmittedForm
          in: query
          required: false
          schema:
            type: boolean
        - name: propertyParams
          in: query
          required: false
          schema:
            type: string
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                type: string
        '404':
          description: No Form Found.
  '/api/v1/resource/framework/forms/form_submission/{formSubmissionId}':
    get:
      tags:
        - Form Information
      operationId: getSubmittedFormsById
      parameters:
        - name: formSubmissionId
          in: path
          required: true
          schema:
            type: integer
            format: int32
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                type: string
  '/api/v1/resource/framework/forms/{id}':
    get:
      tags:
        - Form Information
      summary: Get the Form Information by referenceId
      description: Retrieve a Form by reference info
      operationId: get_1
      parameters:
        - name: id
          in: path
          description: Reference Info to retrieve the Forms
          required: true
          schema:
            type: string
          example: Form
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                type: string
        '404':
          description: No Form Found.
  '/api/v1/resource/framework/forms/schema/{id}':
    get:
      tags:
        - Form Schema Information
      summary: Get the JSON schema for the form version
      description: 'Retrieve a JSON schema for the form version.It is a Design time Service that provides JSON schema of the Form '
      operationId: get_2
      parameters:
        - name: id
          in: path
          description: 'The version number of the JSON schema to retrieve.Latest version: 2.0'
          required: true
          schema:
            type: string
          example: V2
      responses:
        '200':
          description: OK
          content:
            '*/*':
              schema:
                type: string
        '404':
          description: No Form Found.
components:
  schemas:
    JsonRiskCalculationResult:
      type: object
      properties:
        customerId:
          maxLength: 64
          minLength: 0
          type: string
          description: The unique identifier for a customer
          example: '45221'
        formSubmissionId:
          type: integer
          format: int32
        nextReviewDate:
          type: string
          description: 'Next review date this, is configured in the risk matrix and depends on the risk status, it can be empty if there is no configuration in the risk matrix.'
          example: '2020/07/07 10:21:33'
        responseStatus:
          type: string
          description: 'The response status calculated by the Fraud detection module, possible values: ALLOW, BLOCK'
          example: ALLOW
          enum:
            - ALLOW
            - BLOCK
        riskCalculationDate:
          type: string
          description: The date the risk is calculated.
          example: '2020/07/07 10:21:33'
        riskLevel:
          type: integer
          description: This is a long value that represents the risk level.
          format: int64
          example: 300
        riskStatus:
          maxLength: 254
          minLength: 0
          type: string
          description: 'This is a string representing the risk status, the possible values are configured in the risk matrix.'
          example: LOW
    JsonAssessment:
      required:
        - name
        - value
      type: object
      properties:
        name:
          maxLength: 254
          minLength: 0
          type: string
          description: This is mapped as the AssessmentType.name in FCM
          example: Intended Products
        value:
          maxLength: 254
          minLength: 0
          type: string
          description: This is the actual name of the FCM Assessment
          example: Loan
      description: 'List of assessments for the customer, can be empty.'
    JsonCifField:
      required:
        - name
        - value
      type: object
      properties:
        name:
          maxLength: 254
          minLength: 0
          type: string
          description: Name of the dynamic (sytem-specific) field
          example: mail
        value:
          type: string
          description: Actual value of the field for the customer
          example: customer@fcm.com
      description: 'List of customer dynamic fields, can be empty.'
    JsonCustomer:
      required:
        - customerDetails
      type: object
      properties:
        assessments:
          type: array
          description: 'List of assessments for the customer, can be empty.'
          items:
            $ref: '#/components/schemas/JsonAssessment'
        cifFields:
          type: array
          description: 'List of customer dynamic fields, can be empty.'
          items:
            $ref: '#/components/schemas/JsonCifField'
        customerDetails:
          $ref: '#/components/schemas/JsonCustomerDetails'
        sectors:
          $ref: '#/components/schemas/JsonSectors'
      description: 'Full customer data, in json format'
    JsonCustomerDetails:
      required:
        - application
        - closed
        - company
        - coreData1
        - coreData2
        - coreData3
        - coreData4
        - coreData5
        - customerId
        - pep
        - segmentCode
        - typeId
      type: object
      properties:
        address1:
          maxLength: 254
          minLength: 0
          type: string
          description: The first line of the customer's address.
          example: '1285, AVENUE OF THE AMERICAS'
        address2:
          maxLength: 254
          minLength: 0
          type: string
          description: The second line of the customer's address.
          example: 'NEW YORK, NEW YORK'
        application:
          maxLength: 254
          minLength: 0
          type: string
          description: The name of the last application that modified the current customer.
          example: GUI-SectorLinking
        bankId2:
          maxLength: 64
          minLength: 0
          type: string
          description: 'This can be used to store any bank information that fits, it was used before for custom implementations, can be left blank.'
          example: '18001'
        birthCity:
          maxLength: 254
          minLength: 0
          type: string
          description: The customer's birth city.
          example: New York
        birthCountry:
          maxLength: 2
          minLength: 0
          type: string
          description: ISO country code of the country in which the customer was born.
          example: BE
        birthDate:
          type: string
          description: 'The customer''s birth date formatted as : yyyy-MM-dd HH:mm:ss'
          example: '1930-01-10 00:00:00'
        branch:
          maxLength: 32
          minLength: 0
          type: string
          description: The customer's bank branch
          example: GB0010001
        careOf:
          maxLength: 5
          minLength: 0
          type: string
          description: 'This is a legacy field(was used in the old VIVEO profile), but is required in the FCM DB so it can be defaulted to false.'
          example: 'false'
          enum:
            - 'true'
            - 'false'
        city:
          maxLength: 254
          minLength: 0
          type: string
          description: City of residence.
          nullable: true
          example: New York
        closed:
          maxLength: 5
          minLength: 0
          type: string
          description: If true this means that the customer relationship with the bank has terminated(customer no longer active).
          example: 'false'
          enum:
            - 'true'
            - 'false'
        company:
          maxLength: 10
          minLength: 0
          type: string
          description: The customer's company name.
          example: GB0010002
        coreData1:
          maxLength: 22
          minLength: 0
          type: string
          description: 'This is bank specific and it is used to defined customer specific parameters(bank can define their own meaning) it is currently used in the profile rules, if bank doesn''t has a use for this it can be filled with 0.0 as default value.'
          example: '0.5'
        coreData2:
          maxLength: 22
          minLength: 0
          type: string
          description: 'This is bank specific and it is used to defined customer specific parameters(bank can define their own meaning) it is currently used in the profile rules, if bank doesn''t has a use for this it can be filled with 0.0 as default value.'
          example: '0.5'
          default: '0.0'
        coreData3:
          maxLength: 22
          minLength: 0
          type: string
          description: 'This is bank specific and it is used to defined customer specific parameters(bank can define their own meaning) it is currently used in the profile rules, if bank doesn''t has a use for this it can be filled with 0.0 as default value.'
          example: '0.5'
          default: '0.0'
        coreData4:
          maxLength: 22
          minLength: 0
          type: string
          description: 'This is bank specific and it is used to defined customer specific parameters(bank can define their own meaning) it is currently used in the profile rules, if bank doesn''t has a use for this it can be filled with 0.0 as default value.'
          example: '0.5'
          default: '0.0'
        coreData5:
          maxLength: 22
          minLength: 0
          type: string
          description: 'This is bank specific and it is used to defined customer specific parameters(bank can define their own meaning) it is currently used in the profile rules, if bank doesn''t has a use for this it can be filled with 0.0 as default value.'
          example: '0.5'
          default: '0.0'
        country:
          maxLength: 2
          minLength: 0
          type: string
          description: ISO Country code of the country of the customer.
          example: BE
        customerId:
          maxLength: 64
          minLength: 0
          type: string
          description: Unique id for the customer
          example: BE
        firstName:
          maxLength: 256
          minLength: 0
          type: string
          description: First name/Given name of the customer
          example: Jean-Jacques
        fiscalCountry:
          maxLength: 2
          minLength: 0
          type: string
          description: ISO Country code of the fiscal country of the customer.
          example: BE
        name:
          maxLength: 254
          minLength: 0
          type: string
          description: Name (family name) of the customer
          example: Jean-Jacques
        natCountry:
          maxLength: 2
          minLength: 0
          type: string
          description: ISO Country of nationality of the customer.
          example: BE
        nationalId:
          maxLength: 32
          minLength: 0
          type: string
          description: National identifier for the customer in his/her country.
          example: GE5Z4342333
        occupation:
          maxLength: 254
          minLength: 0
          type: string
          description: The occupation of the customer.
          example: Consultant
        passportNumber:
          maxLength: 32
          minLength: 0
          type: string
          description: Passport number for the customer in his/her country.
          example: GE5Z4342333
        pep:
          type: string
          description: Specifies whether the customer is a Politically Exposed Person or not.
          example: 'false'
          enum:
            - 'true'
            - 'false'
        segmentCode:
          maxLength: 254
          minLength: 0
          type: string
          description: 'The code of the customer segment profile, the code meaning is further defined in PRO_SEGMENT FCM table we can tell for example if the customer is an Individual or a Company, the risk calculation will not be done if this is empty.'
          example: '8899'
        socialSecurityNumber:
          maxLength: 32
          minLength: 0
          type: string
          description: Social security number for the customer in his/her country.
          example: GE5Z4342333
        ssnCountry:
          maxLength: 2
          minLength: 0
          type: string
          description: ISO Social Security Number Country of the customer.
          example: BE
        state:
          maxLength: 64
          minLength: 0
          type: string
          description: State of residence of the customer.
          example: Ohio
        telephoneNumberFix:
          maxLength: 32
          minLength: 0
          type: string
          description: Fix telephone number of the customer.
          example: +0430788888342
        telephoneNumberMobile:
          maxLength: 32
          minLength: 0
          type: string
          description: Mobile telephone number of the customer.
          example: +0430788888341
        title:
          maxLength: 32
          minLength: 0
          type: string
          description: Honorific applied to customer.
          example: Sir
        typeId:
          maxLength: 3
          minLength: 0
          type: string
          description: |-
            The type of the entity. If this field is mapped, it takes precedence to the value specified in the <entity type="…"> element.
            When present, this value is used for the message type sent to the scanning engine.
          example: T24
        zipCode:
          maxLength: 32
          minLength: 0
          type: string
          description: Zipcode of the customer's residence address.
          example: 098799
      description: This object contains the actual customer fields.
    JsonSectors:
      type: object
      properties:
        sectorNames:
          uniqueItems: true
          type: array
          description: An array with the FCM Sector(Segment) names the size of each name is limited to 254 characters.
          example:
            - Gambling
            - Agriculture
            - Entertainment
          items:
            type: string
            description: An array with the FCM Sector(Segment) names the size of each name is limited to 254 characters.
            example: '["Gambling","Agriculture","Entertainment"]'
      description: Object containing an array of sector names.
    JsonCifFieldDefinitionResponse:
      type: object
      properties:
        name:
          type: string
        type:
          type: string
    JsonAssessmentResponse:
      type: object
      properties:
        name:
          type: string
        options:
          uniqueItems: true
          type: array
          items:
            type: string
    Answer:
      required:
        - questionKey
      type: object
      properties:
        name:
          type: string
          description: The name of the question that was answered.
          example: Annual income volume
        questionKey:
          type: string
          description: The question key of the question that was answered.
          example: 84687f12-8fe2-4402-9ae3-0530f9e87390
        value:
          type: object
          description: The value that represents the answer.
          example: 10K to 50K
        valueOptionKeys:
          type: array
          description: An array with the answer options as keys for the answered question in case there is a multiple answer question.
          items:
            type: string
            description: An array with the answer options as keys for the answered question in case there is a multiple answer question.
      description: Actual answers to the questions of the form.
    FormSubmit:
      required:
        - answers
        - formReference
      type: object
      properties:
        answers:
          type: array
          description: Actual answers to the questions of the form.
          items:
            $ref: '#/components/schemas/Answer'
        formReference:
          type: string
          description: Reference info identifier of the submitted form.
      description: 'Full answers to the form, including the mandatory form reference'
    CustomerUpdateSuccessResponse:
      type: object
      properties:
        customerId:
          type: string
        responseCode:
          type: integer
          format: int32
        response:
          type: string
    FormStatusRequest:
      type: object
      properties:
        customerId:
          type: string
        formFields:
          type: object
          additionalProperties:
            type: string
        formId:
          type: string
        formType:
          type: string
      description: 'Customer form data, in json format'
    FormUpdateSuccessResponse:
      type: object
      properties:
        customerId:
          type: string
        formType:
          type: string
          enum:
            - CustomerOnboarding
            - EnhancedDueDiligence
        submittedDate:
          type: string
    FormUpdateRequest:
      type: object
      properties:
        properties:
          type: array
          items:
            $ref: '#/components/schemas/StoreItemPropertyRequest'
    StoreItemPropertyRequest:
      type: object
      properties:
        name:
          type: string
        value:
          type: string
    FormSubmissionUpdateResponse:
      type: object
      properties:
        message:
          type: string
        submittedTime:
          type: string
    JsonCustomerStatus:
      required:
        - listName
        - status
      type: object
      properties:
        alertId:
          type: string
          description: Alert Reference
          example: '12345'
        creationDate:
          type: string
          description: Watchlist name
          format: yyyy-MM-dd
          example: '2019-12-23'
        lastEditDate:
          type: string
          description: Last Edit Date
          format: yyyy-MM-dd
          example: '2019-12-23'
        listName:
          type: string
          description: Watchlist name
          example: OFAC
        nextReviewDate:
          type: string
          description: Link Status next review date
          format: yyyy-MM-dd
          example: '2020-12-22'
        status:
          type: string
          description: Link Status Name
          example: IsInWatchlist
      description: List of customer watchlist link status
    JsonCustomerStatusesResponse:
      type: object
      properties:
        count:
          type: integer
          description: Total Records
          format: int32
          example: 1
        customerStatuses:
          type: array
          description: List of customer watchlist link status
          items:
            $ref: '#/components/schemas/JsonCustomerStatus'
    JsonError:
      type: object
      properties:
        errorMessage:
          type: string
        errorType:
          type: string
    JsonErrorResponse:
      type: object
      properties:
        errorCount:
          type: integer
          format: int32
        errors:
          type: array
          items:
            $ref: '#/components/schemas/JsonError'
    JsonResponse:
      type: object
  securitySchemes:
    basicScheme:
      type: http
      scheme: basic
