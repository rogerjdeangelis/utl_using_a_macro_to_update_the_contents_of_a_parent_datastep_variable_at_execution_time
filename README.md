# utl_using_a_macro_to_update_the_contents_of_a_parent_datastep_variable_at_execution_time
Academic: Using a macro to update the contents of a parent datastep variable at execution time  The parent and child share a common addrress. I did get warning but code works. Passing by reference(address) usually means you want to access or change wha is at that address.  In this code we change Alices age in the parent datastep from 13 to 15 using a subroutine macro and    common storage

    ```  Academic: Using a macro to update the contents of a parent datastep variable at execution time                                                               ```
    ```                                                                                                                                                               ```
    ```  The parent and child share a common addrress. I did get warning but code works.                                                                              ```
    ```  Passing by reference(address) usually means you want to access or change wha is at that address.                                                             ```
    ```                                                                                                                                                               ```
    ```  HERE IS THE CODE                                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```     In this code we change Alices age in the parent datastep from 13 to 15 using a subroutine macro and                                                       ```
    ```     common storage                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```     WORKING CODE                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```     %macro parent;                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```       set sashelp.class(where=(name="&name"));                                                                                                                ```
    ```                                                                                                                                                               ```
    ```       %common(age);                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```       put "parent " age=;  * 13;                                                                                                                              ```
    ```       %child;              * * the child upates the variable age in the parent;                                                                               ```
    ```       put "parent " age=;  * 15;                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```       /*                                                                                                                                                      ```
    ```       parent AGE=13                                                                                                                                           ```
    ```       parent AGE=15                                                                                                                                           ```
    ```       */                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```    %mend parent;                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```    %parent(name=Alice,age=15);                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```  HAVE                                                                                                                                                         ```
    ```  ====                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  SASHELP.CLASS                                                                                                                                                ```
    ```                                   |   RULE                                                                                                                    ```
    ```  Obs    NAME       SEX    AGE     |                                                                                                                           ```
    ```                                   |                                                                                                                           ```
    ```    1    Alfred      M      14     |                                                                                                                           ```
    ```    2    Alice       F      13     |   Change age to 15                                                                                                        ```
    ```    3    Barbara     F      13     |                                                                                                                           ```
    ```   ....                                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  WANT (use a macro to change age within one datastep)                                                                                                         ```
    ```  =====================================================                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  WOR.CLASS                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  Obs    NAME       SEX    AGE                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```    1    Alfred      M      14                                                                                                                                 ```
    ```    2    Alice       F      15    * changed                                                                                                                    ```
    ```    3    Barbara     F      13                                                                                                                                 ```
    ```   ....                                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  https://communities.sas.com/t5/SAS-Procedures/Passing-a-variable-into-a-macro-as-a-value/m-p/409419                                                          ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```     * jusst use sashelp.class;                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  * clear environment - put REPLACE THIS in the paste buffer;                                                                                                  ```
    ```  filename clp clipbrd;                                                                                                                                        ```
    ```  data _null_;                                                                                                                                                 ```
    ```    file clp;                                                                                                                                                  ```
    ```    put "REPLACE THIS";                                                                                                                                        ```
    ```  run;quit;                                                                                                                                                    ```
    ```  filename clp clear;                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  /* as a side note "x clip" will clear the clipboard  */                                                                                                      ```
    ```                                                                                                                                                               ```
    ```  options nofullstimer;                                                                                                                                        ```
    ```  proc datasets lib=work kill;                                                                                                                                 ```
    ```  run;quit;                                                                                                                                                    ```
    ```  %symdel adrAge age /nowarn;                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  * in 9.4M2 a child macro cannot see the parent macro symbol table.                                                                                           ```
    ```    I had to use th clipboard to send the address of age to the child macro.                                                                                   ```
    ```                                                                                                                                                               ```
    ```  %macro common(age);                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```    adrAge=put(addrlong(age),hex16.);                                                                                                                          ```
    ```    call symputx("adrage",adrage,"G");                                                                                                                         ```
    ```    rc=dosubl('filename clp clipbrd;data _null_;file clp;put "&adrage";run;quit;filename clp clear;run;quit;');                                                ```
    ```                                                                                                                                                               ```
    ```  %mend common;                                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  %macro child;                                                                                                                                                ```
    ```    rc=dosubl('data _null_;infile clp;input adrage $char16.;call symputx("adrage",adrage);                                                                     ```
    ```      filename cl2 clear;run;quit;');                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```    adrage=symget("adrage");                                                                                                                                   ```
    ```    adr=input(adrage,$hex16.);                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```    age=input(peekclong(adr,8),rb8.);                                                                                                                          ```
    ```    call pokelong(put(&age,rb8.),adr,8);                                                                                                                       ```
    ```  %mend child;                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  %macro parent(name=,age=);                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```     data want(drop=rc adr adrAge);                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```       set sashelp.class(where=(name="&name"));                                                                                                                ```
    ```                                                                                                                                                               ```
    ```       put "*** before  " age=;                                                                                                                                ```
    ```       %common(&age);                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```       %child;   * the child upates the variable age in the parent;                                                                                            ```
    ```                                                                                                                                                               ```
    ```       put "*** after "   age=;                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```     run;quit;                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```  %mend parent;                                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```  %parent(name=Alice,age=15);                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```

