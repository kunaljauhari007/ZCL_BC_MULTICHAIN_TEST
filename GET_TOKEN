  METHOD get_token.
    DATA: lo_http_client TYPE REF TO if_http_client.
    DATA: response TYPE string,
          lv_url   TYPE string.
    CONSTANTS: lv_initial_url TYPE string VALUE 'https://sapitcfd.authentication.sap.hana.ondemand.com/oauth/token?grant_type=client_credentials',
               lv_auth        TYPE string VALUE 'Basic c2ItNmQ1YTRmYmEtYTVlYi00OTc2LThmNWQtMGE4NmU5NmFlNTJmIWI1Nzd8bmEtNTRiYzI1ZjMtZjkzNy00MGI3LThiMzMtZmZlMjQwODk5Y2YwIWIzNDI6TGMrcXBNT2dqUUhnUy9wci8vKy92cDh0SWZjPQ=='.


    "create HTTP client by url
    CALL METHOD cl_http_client=>create_by_url
      EXPORTING
        url                = lv_initial_url
      IMPORTING
        client             = lo_http_client
      EXCEPTIONS
        argument_not_found = 1
        plugin_not_active  = 2
        internal_error     = 3
        OTHERS             = 4.

    "Available API Endpoints
    "https://blockchain-service.cfapps.sap.hana.ondemand.com/blockchain/proofOfHistory/api/v1
    "https://blockchain-service.cfapps.eu10.hana.ondemand.com/blockchain/proofOfHistory/api/v1
    "https://blockchain-service.cfapps.us10.hana.ondemand.com/blockchain/proofOfHistory/api/v1

    IF sy-subrc <> 0.
      "error handling
    ENDIF.

    "setting request method
    lo_http_client->request->set_method('GET').

    "adding headers
    lo_http_client->request->set_header_field( name = 'Authorization' value = lv_auth ).


    "Available Security Schemes for productive API Endpoints
    "OAuth 2.0

    CALL METHOD lo_http_client->send
      EXCEPTIONS
        http_communication_failure = 1
        http_invalid_state         = 2
        http_processing_failed     = 3
        http_invalid_timeout       = 4
        OTHERS                     = 5.

    IF sy-subrc = 0.
      CALL METHOD lo_http_client->receive
        EXCEPTIONS
          http_communication_failure = 1
          http_invalid_state         = 2
          http_processing_failed     = 3
          OTHERS                     = 5.
    ENDIF.

    IF sy-subrc <> 0.
      "error handling
    ENDIF.

    response = lo_http_client->response->get_cdata( ).

   GV_TOKEN = response.
  ENDMETHOD.
