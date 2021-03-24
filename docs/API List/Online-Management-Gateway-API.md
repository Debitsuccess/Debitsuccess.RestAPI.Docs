{
  "openapi" : "3.0.0",
  "info" : {
    "title" : "Online Management Gateway API",
    "description" : "---\n## Overview\nThe online management gateway API allow for the creation of account templates. The account templates are used to signup new customer via Debitsuccess Online management gateway web application.\n\n## Web Application\nOnline management gateway Web application\n\n\*\*Test Envrionment\*\*\\\nhttps://oc-test.debitsuccess.com/DirectEntry/DirectDebitRequest/Form?templateid=\n\n\*\*Live Envrionment\*\*\\\nhttps://oc.debitsuccess.com/DirectEntry/DirectDebitRequest/Form?templateid=\n\n## Online Management Gateway API\n\*\*Test Environment\*\*\\\nhttps://oc-test.debitsuccess.com/DirectEntry/api/v1.0/accounttemplates\n\n\*\*Live Environment\*\*\\\nhttps://oc.debitsuccess.com/DirectEntry/api/v1.0/accounttemplates\n\n## Authentication \nPlease visit [Debitsuccess Identity Service](https://app.swaggerhub.com/apis/debitsuccess/DebitsuccessIdentity/1.0.0) \n",
    "version" : "1.0.0"
  },
  "servers" : [ {
    "url" : "/"
  } ],
  "tags" : [ {
    "name" : "Account Template"
  } ],
  "paths" : {
    "/directEntry/api/v1.0/accounttemplates" : {
      "post" : {
        "tags" : [ "Account Template" ],
        "description" : "Creates an account template that can later be used on Debitsuccess Online \nManagement Getaway to sign up new customers. \*\*Note\*\* - The \*\*customerdetails\*\* field in the request must be sent as base64 encoded string of Json object.\n",
        "requestBody" : {
          "content" : {
            "application/json" : {
              "schema" : {
                "$ref" : "#/components/schemas/AccountTemplate"
              }
            }
          }
        },
        "responses" : {
          "200" : {
            "description" : "Successful Request",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/inline_response_200"
                }
              }
            }
          },
          "400" : {
            "description" : "Unsuccessful Request",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/inline_response_400"
                }
              }
            }
          },
          "401" : {
            "description" : "Unauthorized - Occurs when the authorization token provided is either expired or invalid.",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/inline_response_401"
                }
              }
            }
          }
        }
      },
      "delete" : {
        "tags" : [ "Account Template" ],
        "description" : "Allows for the deletion of account templates.",
        "parameters" : [ {
          "name" : "accountTemplateId",
          "in" : "path",
          "description" : "The id of the template you would like to delete",
          "required" : true,
          "style" : "simple",
          "explode" : false,
          "schema" : {
            "type" : "string"
          }
        }, {
          "name" : "authorization",
          "in" : "header",
          "description" : "JWT token using Bearer authorization scheme",
          "required" : true,
          "style" : "simple",
          "explode" : false,
          "schema" : {
            "type" : "string"
          }
        } ],
        "responses" : {
          "200" : {
            "description" : "Successful Request",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/inline_response_200_1"
                }
              }
            }
          },
          "400" : {
            "description" : "Unsuccessful Request",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/inline_response_400_1"
                }
              }
            }
          },
          "401" : {
            "description" : "Unauthorized - Occurs when the authorization token provided is either expired or invalid.",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/inline_response_401"
                }
              }
            }
          }
        }
      }
    },
    "/directEntry/api/v1.0/diagnostics/ping" : {
      "get" : {
        "tags" : [ "Account Template" ],
        "description" : "Used to determine whether this api is online.",
        "parameters" : [ {
          "name" : "authorization",
          "in" : "header",
          "description" : "JWT token using Bearer authorization scheme",
          "required" : true,
          "style" : "simple",
          "explode" : false,
          "schema" : {
            "type" : "string"
          }
        } ],
        "responses" : {
          "200" : {
            "description" : "Successful Request",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/inline_response_200_2"
                }
              }
            }
          },
          "401" : {
            "description" : "Unauthorized - Occurs when the authorization token provided is either expired or invalid.",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/inline_response_401"
                }
              }
            }
          }
        }
      }
    }
  },
  "components" : {
    "schemas" : {
      "AccountTemplate" : {
        "required" : [ "benefits", "businessId", "ddrTemplate", "defaultFrequency", "description", "firstPaymentDateMin", "installment", "isTerm", "name", "term", "termType" ],
        "type" : "object",
        "properties" : {
          "name" : {
            "type" : "string",
            "description" : "The name of the template.",
            "example" : "12 payment ongoing membership"
          },
          "paymentOption" : {
            "type" : "string",
            "description" : "0 = Bank Account + Credit Card, 1 = Bank Account, 2 = Credit Card",
            "example" : "0"
          },
          "term" : {
            "type" : "string",
            "description" : "Minimum term in months or payments. Min 0 when TermType is Months Min 1 when Termtype is Payment max 999.",
            "example" : "12"
          },
          "termType" : {
            "type" : "string",
            "description" : "M - Months, P - Payments",
            "example" : "P"
          },
          "isTerm" : {
            "type" : "boolean",
            "description" : "Type of agreement false - OnGoing true - Fix Term",
            "example" : false
          },
          "accountCode" : {
            "type" : "string",
            "description" : "Maximum 50 characters.",
            "example" : "Sale 3209"
          },
          "totalAmount" : {
            "type" : "number",
            "description" : "Total value of recurring payments to be collected for account. For TermType = 'p' - Term \* Instalment >= TotalAmount >= Term - 1 \* Instalment = totalAmount. For TermType = 'm'  Term \* Instalment >= TotalAmount >= One Instalment = totalAmount.",
            "example" : 10.00
          },
          "overrideEstFee" : {
            "type" : "boolean",
            "description" : "true – Facility pays means 0$, false – Use facility account settings (by default) means using the setting in ELK(10$)",
            "example" : false
          },
          "ddrTemplate" : {
            "type" : "string",
            "description" : "OMG brand template unique-identifier",
            "example" : "8afc3d5a-e647-402d-89de-7ad9c99529d9"
          },
          "businessId" : {
            "type" : "string",
            "description" : "1-6 characters Debitsuccess business id. The account template will be assigned to this business.",
            "example" : "TST4"
          },
          "isCustomFrequency" : {
            "type" : "boolean",
            "description" : "if true allows customer to select frequency and first payment date when signing up.",
            "example" : false
          },
          "installment" : {
            "type" : "number",
            "description" : "installment amount value. Accepts 0 value when isCustomFrequency is true.",
            "example" : 10.00
          },
          "allowableFrequencies" : {
            "type" : "string",
            "description" : "required when isCustomFrequency is true. Options- WK -Weekly,FN - Fortnightly,FW - FourWeekly, MN - Monthly, QT – Quarterly. This field can accept multiple comma-separated frequency.",
            "example" : "WK,FN,MN"
          },
          "defaultFrequency" : {
            "type" : "string",
            "description" : "Options- WK -Weekly,FN - Fortnightly,FW - FourWeekly, MN - Monthly, QT – Quarterly.",
            "example" : "WK"
          },
          "billingFee" : {
            "type" : "number",
            "description" : ">=0 and <100,000.00 The value in this field is added to the Instalment amount and is debited \nevery frequency from the customer's account.\n",
            "example" : 0
          },
          "additionalOneOffPayment" : {
            "type" : "number",
            "description" : ">=0 and <100,000.00 Amount of initial one-off payment, can be Joining fee or any other one-off fees that the facility wants to debit from the user.   \n",
            "example" : 0
          },
          "joiningFeeIsFirstInstalment" : {
            "type" : "boolean",
            "description" : "true – Treat joining Fee As First Instalment, false – by default.",
            "example" : false
          },
          "contractStartDate" : {
            "type" : "string",
            "description" : "The date in this field will be treated as the date of the first payment, establishment fee will be taken if applicable."
          },
          "firstPaymentDateMin" : {
            "type" : "number",
            "description" : "The Days until first instalment and it reflects the First payment date ContractStartDate = Current Date + FirstPaymentDateMin. If customer is allowed to choose start date and frequency (isCustomFrequency = true) then the date may not be before Current Date + FirstPaymentDateMin.",
            "example" : 1
          },
          "benefits" : {
            "type" : "string",
            "description" : "The Description is displayed on the DDR form for the customers.",
            "example" : "benefit"
          },
          "description" : {
            "type" : "string",
            "description" : "The Description for internal Use Only. Max 2000 characters.",
            "example" : "Account template for 12 month ongoing membership"
          },
          "specialConditions" : {
            "type" : "string",
            "description" : "Max 2000 characters.",
            "example" : "specialConditions"
          },
          "templateEndDate" : {
            "type" : "string",
            "description" : "The date when the customer link will be deactivated. By default, will be calculated as Template creation date + 5 days.",
            "example" : "2020/12/01"
          },
          "promoCode" : {
            "type" : "string",
            "example" : "Promocode"
          },
          "isProRata" : {
            "type" : "boolean",
            "description" : "true - Pro-rata final payment. Last payment will be less than instalments to make sure that the total amount of payments will not be changed. false - Divide the payment equally. The total value will be divided by the number of payments that will be calculated based on the  customer-selected frequency",
            "example" : false
          },
          "AllowMinors" : {
            "type" : "boolean",
            "description" : "true - Allow users to sign up Minors and will create omg template with Minor and Guarantor information. false(by default) - Minor will not be allowed for the template generated.",
            "example" : false
          },
          "externalAccountReferenceNo" : {
            "type" : "string",
            "description" : "External Account Identifier",
            "example" : "eba09c3c-3f67-11e8-b467-0ed5f89f718b"
          },
          "customerDetails" : {
            "$ref" : "#/components/schemas/CustomerDetails"
          }
        }
      },
      "CustomerDetails" : {
        "required" : [ "dob", "email", "firstName", "gender", "lastName", "postcode", "state", "streetAddress", "suburb" ],
        "type" : "object",
        "properties" : {
          "firstName" : {
            "maximum" : 40,
            "type" : "string",
            "example" : "John"
          },
          "lastName" : {
            "maximum" : 40,
            "type" : "string",
            "example" : "Doe"
          },
          "dob" : {
            "type" : "string",
            "format" : "dd/mm/yyyy, yyyy-mm-dd, yyyy/mm/dd",
            "example" : "1991-12-19"
          },
          "gender" : {
            "type" : "integer",
            "description" : "0 = male 1 = female 2 = other",
            "example" : 1
          },
          "driversLicenseOrMedicareNumber" : {
            "maximum" : 40,
            "type" : "string",
            "example" : "SD9999"
          },
          "streetAddress" : {
            "maximum" : 40,
            "type" : "string",
            "example" : "5 The warehouse road"
          },
          "suburb" : {
            "maximum" : 40,
            "type" : "string",
            "example" : "NorthCote"
          },
          "postcode" : {
            "maximum" : 4,
            "type" : "string",
            "example" : "5685"
          },
          "city" : {
            "type" : "string",
            "example" : "Auckland"
          },
          "state" : {
            "maximum" : 4,
            "type" : "string",
            "example" : "Auck"
          },
          "email" : {
            "type" : "string",
            "example" : "John.Doe@gmail.com"
          },
          "phoneHome" : {
            "type" : "string",
            "description" : "One of phoneHome, phoneWork, phoneMobile , phoneEmergency is required.",
            "example" : "09-1111111"
          },
          "phoneWork" : {
            "type" : "string",
            "description" : "One of phoneHome, phoneWork, phoneMobile , phoneEmergency is required.",
            "example" : "094213422"
          },
          "phoneMobile" : {
            "type" : "string",
            "description" : "One of phoneHome, phoneWork, phoneMobile , phoneEmergency is required.",
            "example" : "021324223"
          },
          "phoneEmergency" : {
            "type" : "string",
            "description" : "One of phoneHome, phoneWork, phoneMobile , phoneEmergency is required.",
            "example" : "233341221"
          },
          "emergencyContactName" : {
            "type" : "string",
            "example" : "John Doe"
          }
        }
      },
      "inline_response_200" : {
        "type" : "object",
        "properties" : {
          "successful" : {
            "type" : "boolean",
            "description" : "Indicator to determine whether the request has been successfully processed",
            "example" : true
          },
          "errorMessage" : {
            "type" : "array",
            "description" : "List of error messages",
            "items" : {
              "type" : "string"
            }
          },
          "successMessage" : {
            "type" : "array",
            "description" : "List of successful messages",
            "items" : {
              "type" : "string",
              "example" : "The account template was successfully created."
            }
          },
          "accountTemplateId" : {
            "type" : "string",
            "example" : "91e52753-5c7c-4a0e-9e67-81cc5575db46"
          }
        }
      },
      "inline_response_400" : {
        "type" : "object",
        "properties" : {
          "successful" : {
            "type" : "boolean",
            "description" : "Indicator to determine whether the request has been successfully processed",
            "example" : false
          },
          "errorMessage" : {
            "type" : "array",
            "description" : "List of error messages",
            "items" : {
              "type" : "string",
              "example" : "Validation error messages"
            }
          },
          "successMessage" : {
            "type" : "array",
            "description" : "List of successful messages",
            "items" : {
              "type" : "string"
            }
          },
          "accountTemplateId" : {
            "type" : "string",
            "example" : "00000000-0000-0000-0000-000000000000"
          }
        }
      },
      "inline_response_401" : {
        "type" : "object",
        "properties" : {
          "message" : {
            "type" : "string",
            "description" : "Indicator to determine whether the request has been successfully processed",
            "example" : "Authorization has been denied for this request."
          }
        }
      },
      "inline_response_200_1" : {
        "type" : "object",
        "properties" : {
          "successful" : {
            "type" : "boolean",
            "description" : "Indicator to determine whether the request has been successfully processed",
            "example" : true
          },
          "errorMessage" : {
            "type" : "array",
            "description" : "List of error messages",
            "items" : {
              "type" : "string"
            }
          },
          "successMessage" : {
            "type" : "array",
            "description" : "List of successful messages",
            "items" : {
              "type" : "string",
              "example" : "The account template was successfully deleted."
            }
          },
          "accountTemplateId" : {
            "type" : "string",
            "example" : "00000000-0000-0000-0000-000000000000"
          }
        }
      },
      "inline_response_400_1" : {
        "type" : "object",
        "properties" : {
          "successful" : {
            "type" : "boolean",
            "description" : "Indicator to determine whether the request has been successfully processed",
            "example" : false
          },
          "errorMessage" : {
            "type" : "array",
            "description" : "List of error messages",
            "items" : {
              "type" : "string",
              "example" : "This account template does not exist."
            }
          },
          "successMessage" : {
            "type" : "array",
            "description" : "List of successful messages",
            "items" : {
              "type" : "string"
            }
          },
          "accountTemplateId" : {
            "type" : "string",
            "example" : "00000000-0000-0000-0000-000000000000"
          }
        }
      },
      "inline_response_200_2" : {
        "type" : "object",
        "properties" : {
          "successful" : {
            "type" : "boolean",
            "description" : "Indicator to determine whether the request has been successfully processed",
            "example" : true
          },
          "errorMessage" : {
            "type" : "array",
            "description" : "List of error messages",
            "items" : {
              "type" : "string"
            }
          },
          "successMessage" : {
            "type" : "array",
            "description" : "List of successful messages",
            "items" : {
              "type" : "string"
            }
          },
          "accountTemplateId" : {
            "type" : "string",
            "example" : "00000000-0000-0000-0000-000000000000"
          }
        }
      }
    },
    "responses" : {
      "Success" : {
        "description" : "Successful Request",
        "content" : {
          "application/json" : {
            "schema" : {
              "type" : "object",
              "properties" : {
                "access_token" : {
                  "type" : "string",
                  "description" : "JWT cess token that can be used for the API requested in the scope.",
                  "example" : "eyJhbGciOiJSUzI1NiIsImtpZCI6IjRGMzhGRUYyODI5NzZGNzdFQkU3"
                },
                "expires_in" : {
                  "type" : "string",
                  "description" : "token expiry time. Default 1 hour.",
                  "example" : "3600"
                },
                "token_type" : {
                  "type" : "string",
                  "example" : "Bearer"
                }
              }
            }
          }
        }
      },
      "Unsuccessful" : {
        "description" : "Unsuccessful Request",
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/inline_response_400_1"
            }
          }
        }
      },
      "Unsuccessful-Validation" : {
        "description" : "Unsuccessful Request",
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/inline_response_400"
            }
          }
        }
      },
      "Successful-deletion" : {
        "description" : "Successful Request",
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/inline_response_200_1"
            }
          }
        }
      },
      "Successful-creation" : {
        "description" : "Successful Request",
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/inline_response_200"
            }
          }
        }
      },
      "Successful-ping" : {
        "description" : "Successful Request",
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/inline_response_200_2"
            }
          }
        }
      },
      "Unauthorised-Error" : {
        "description" : "Unauthorized - Occurs when the authorization token provided is either expired or invalid.",
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/inline_response_401"
            }
          }
        }
      },
      "Validation-Error" : {
        "description" : "Bad Request - Request validation error, The response message will vary depending on the cause.",
        "content" : {
          "application/json" : {
            "schema" : {
              "type" : "object",
              "properties" : {
                "error" : {
                  "type" : "string",
                  "description" : "The error response can include any value that is described in the example.",
                  "example" : "unsupported_grant_type,invalid_scope,invalid_client."
                }
              }
            }
          }
        }
      }
    },
    "parameters" : {
      "Authorization" : {
        "name" : "authorization",
        "in" : "header",
        "description" : "JWT token using Bearer authorization scheme",
        "required" : true,
        "style" : "simple",
        "explode" : false,
        "schema" : {
          "type" : "string"
        }
      }
    },
    "securitySchemes" : {
      "petstore_auth" : {
        "type" : "oauth2",
        "flows" : {
          "implicit" : {
            "authorizationUrl" : "http://petstore.swagger.io/oauth/dialog",
            "scopes" : {
              "write:pets" : "modify pets in your account",
              "read:pets" : "read your pets"
            }
          }
        }
      },
      "api_key" : {
        "type" : "apiKey",
        "name" : "api_key",
        "in" : "header"
      }
    }
  }
}Related Articles

label = "omg"falsefalse



*****

[[category.storage-team]] 
[[category.confluence]] 