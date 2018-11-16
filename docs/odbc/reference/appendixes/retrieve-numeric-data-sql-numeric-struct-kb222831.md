---
title: Recuperar datos numéricos con SQL_NUMERIC_STRUCT | Microsoft Docs
description: C/C ++ mediante ODBC recupera el tipo de datos numérico de SQL Server con SQL_NUMERIC_STRUCT, relacionados con SQL_C_NUMERIC.
authors: MightyPen
manager: craigg
editor: ''
ms.prod: sql
ms.technology: ''
ms.devlang: C++
ms.topic: conceptual
ms.custom: ''
ms.date: 07/13/2017
ms.author: genemi
ms.openlocfilehash: a4d6545deb5431322d2bd6bf5f8a42de7cfc8008
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51665974"
---
# <a name="retrieve-numeric-data-with-sqlnumericstruct"></a>Recuperar datos numéricos con SQL\_numérico\_STRUCT

En este artículo se describe cómo recuperar datos numéricos en el controlador ODBC de SQL Server en una estructura numérica. También se describe cómo obtener los valores correctos con precisión específica y valores de escala.

Este tipo de datos permite a las aplicaciones administrar directamente los datos numéricos. Alrededor del año 2003, ODBC 3.0 introdujo un nuevo tipo de datos ODBC C, identificado por **SQL\_C\_numérico**. Este tipo de datos sigue siendo pertinente a partir de 2017.

El búfer de C que se utiliza tiene la definición de tipo de **SQL\_numérico\_STRUCT**. Esta estructura tiene campos para almacenar la precisión, escala, inicio de sesión y el valor de los datos numéricos. El propio valor se almacena como un entero de escalado con el principio del byte menos significativo en la posición más a la izquierda. 

El artículo [tipos de datos C](c-data-types.md) proporciona más información sobre el formato y el uso de SQL\_numérico\_STRUCT. Por lo general el [apéndice D](appendix-d-data-types.md) de referencia del programador de ODBC 3.0 se describen los tipos de datos.


## <a name="sqlnumericstruct-overview"></a>SQL\_numérico\_información general STRUCT


El código SQL\_numérico\_STRUCT se define en el archivo de encabezado sqltypes.h como sigue:


``` C
#define SQL_MAX_NUMERIC_LEN    16
typedef struct tagSQL_NUMERIC_STRUCT
{
   SQLCHAR    precision;
   SQLSCHAR   scale;
   SQLCHAR    sign;   /* 1 if positive, 0 if negative */
   SQLCHAR    val[SQL_MAX_NUMERIC_LEN];
} SQL_NUMERIC_STRUCT;
```

            
Los campos de precisión y escala de la estructura numérica nunca se usan para la entrada desde una aplicación, solo para la salida desde el controlador a la aplicación.

El controlador utiliza la precisión predeterminada (definido por el controlador) y la escala de predeterminado (0) cada vez que la devolución de datos a la aplicación. A menos que la aplicación especifica los valores de precisión y escala, el controlador supone el valor predeterminado y trunca la parte decimal de los datos numéricos.

## <a name="sqlnumericstruct-code-sample"></a>SQL\_numérico\_ejemplo de código de estructura

Este ejemplo de código muestra cómo para:

- Establezca la precisión.
- Establezca la escala.
- Recuperar los valores correctos. 

> [!Note]
> CUALQUIER USO DEL CÓDIGO PROPORCIONADO EN ESTE ARTÍCULO QUEDA BAJO SU RESPONSABILIDAD. 
>
> Microsoft proporciona estos ejemplos de código "tal cual" sin garantía de ningún tipo, ya sea expresa o implícita, incluidas sin limitación las garantías implícitas de comerciabilidad e idoneidad para un propósito específico.

``` C
#include <stdio.h>
#include <string.h>
#include <conio.h>
#include <stdlib.h>
#include <ctype.h>
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

#define MAXDSN       25
#define MAXUID       25
#define MAXAUTHSTR   25
#define MAXBUFLEN   255

SQLHENV     henv   = SQL_NULL_HENV;
SQLHDBC     hdbc1  = SQL_NULL_HDBC;     
SQLHSTMT    hstmt1 = SQL_NULL_HSTMT;
SQLHDESC    hdesc  = NULL;


SQL_NUMERIC_STRUCT NumStr;

int main()
{
   RETCODE retcode;

//Change the values below as appropriate to make a successful connection.
//szDSN: DataSourceName, szUID=userid, szAuthStr: password

UCHAR szDSN[MAXDSN+1] = "sql33",szUID[MAXUID+1]="sa", szAuthStr[MAXAUTHSTR+1] = "";
SQLINTEGER strlen1;
SQLINTEGER a;
int i,sign =1;
long myvalue, divisor;
float final_val;
   
// Allocate the Environment handle. Set the Env attribute, allocate the
//connection handle, connect to the database and allocate the statement //handle.

retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);
retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION,(SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);
retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);
retcode = SQLConnect(hdbc1, szDSN,SQL_NTS,szUID,SQL_NTS,szAuthStr,SQL_NTS);
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);

// Execute the select statement. Here it is assumed that numeric_test
//table is created using the following statements:

// Create table numeric_test (col1 numeric(5,3))
//insert into numeric_test values (25.212)

retcode = SQLExecDirect(hstmt1,(UCHAR *)"select * from numeric_test",SQL_NTS);

// Use SQLBindCol to bind the NumStr to the column that is being retrieved.

retcode = SQLBindCol(hstmt1,1,SQL_C_NUMERIC,&NumStr,19,&strlen1);

// Get the application row descriptor for the statement handle using
//SQLGetStmtAttr.

retcode = SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_ROW_DESC,&hdesc, 0, NULL);

// You can either use SQLSetDescRec or SQLSetDescField when using
// SQLBindCol. However, if you prefer to call SQLGetData, you have to
// call SQLSetDescField instead of SQLSetDescRec. For more information on
// descriptors, please refer to the ODBC 3.0 Programmers reference or
// your Online documentation.

//Used when using SQLSetDescRec
//a=b=sizeof(NumStr);

// Set the datatype, precision and scale fields of the descriptor for the 
//numeric column. Otherwise the default precision (driver defined) and 
//scale (0) are returned.

// In this case, the table contains only one column, hence the second 
//parameter contains one. Zero applies to bookmark columns. Please check 
//the programmers guide for more information.

//retcode=SQLSetDescRec(hdesc,1,SQL_NUMERIC,NULL,sizeof(NumStr),5,3,&NumStr,&a,&b);

retcode = SQLSetDescField (hdesc,1,SQL_DESC_TYPE,(VOID*)SQL_C_NUMERIC,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_PRECISION,(VOID*) 5,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_SCALE,(VOID*) 3,0);
    
// Initialize the val array in the numeric structure.

memset(NumStr.val,0,16);
   
// Call SQLFetch to fetch the first record.

while((retcode =SQLFetch(hstmt1)) != SQL_NO_DATA)
  {
// Notice that the TargetType (3rd Parameter) is SQL_ARD_TYPE, which  
//forces the driver to use the Application Row Descriptor with the 
//specified scale and precision.

   retcode = SQLGetData(hstmt1, 1, SQL_ARD_TYPE, &NumStr, 19, &a); 

// Check for null indicator.

   if ( SQL_NULL_DATA == a )
   {
   printf( "The final value: NULL\n" );
   continue;
   }

// Call to convert the little endian mode data into numeric data.

   myvalue = strtohextoval();

// The returned value in the above code is scaled to the value specified
//in the scale field of the numeric structure. For example 25.212 would
//be returned as 25212. The scale in this case is 3 hence the integer 
//value needs to be divided by 1000.

   divisor = 1;
   if(NumStr.scale > 0)
     {
    for (i=0;i< NumStr.scale; i++)   
         divisor = divisor * 10;
     }
   final_val =  (float) myvalue /(float) divisor;

// Examine the sign value returned in the sign field for the numeric
//structure.
//NOTE: The ODBC 3.0 spec required drivers to return the sign as 
//1 for positive numbers and 2 for negative number. This was changed in the
//ODBC 3.5 spec to return 0 for negative instead of 2.

      if(!NumStr.sign) sign = -1;
      else sign  =1;

   final_val *= sign;
   printf("The final value: %f\n",final_val);
    }

   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA_FOUND);

   /* clean up */ 
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);
   SQLDisconnect(hdbc1);
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
   return(0);
}
```


### <a name="interim-results"></a>Resultados provisionales:


```
//  C  ==> 12 * 1    =     12
//  7  ==> 07 * 16   =    112
//  2  ==> 02 * 256  =    512
//  6  ==> 06 * 4096 =  24576
===============================
                 Sum =  25212
```


En la estructura numérica, el campo val es una matriz de caracteres de 16 elementos. Por ejemplo, se escala 25.212 a 25212 y la escala es 3. En formato hexadecimal, este número sería 627C.

El controlador devuelve los siguientes elementos:

- El carácter equivalente de C de 7, que es ' |' (canalización) en el primer elemento de la matriz de caracteres.
- El equivalente de 62, que es 'b' en el segundo elemento.
- El resto de los elementos de matriz contiene ceros, por lo que el búfer contiene ' | b\0'.

Ahora el desafío consiste en construir el entero escalado fuera de esta matriz de cadenas. Cada carácter de la cadena se corresponde con dos dígitos hexadecimales, por ejemplo, menos significativo (LSD) y dígitos más significativos (MSD). El valor entero escalado se puede generar mediante la multiplicación de cada dígito (LSD & MSD) con un múltiplo de 16, comenzando por 1.

Código que implementa la conversión desde el modo little-endian en el entero escalado. Es responsabilidad del desarrollador de aplicaciones para implementar esta funcionalidad. El siguiente ejemplo de código es solo una de las muchas maneras posibles.


``` C
long strtohextoval()
{
    long val=0,value=0;
    int i=1,last=1,current;
    int a=0,b=0;

        for(i=0;i<=15;i++)
        {
         current = (int) NumStr.val[i];
         a= current % 16; //Obtain LSD
         b= current / 16; //Obtain MSD
            
         value += last* a;   
         last = last * 16;   
         value += last* b;
         last = last * 16;   
        }
     return value;
}
```


### <a name="applies-to-versions"></a>Se aplica a las versiones


La información anterior sobre SQL\_numérico\_STRUCT se aplica a las siguientes versiones de producto:

- Controlador ODBC de Microsoft para Microsoft SQL Server 3.7
- Microsoft Data Access Components 2.1
- Microsoft Data Access Components 2.5
- Microsoft Data Access Components 2.6
- Microsoft Data Access Components 2.7


## <a name="sqlcnumeric-overview"></a>SQL\_C\_Introducción a numérico


El programa de ejemplo siguiente muestra el uso de SQL\_C\_numérico, insertando 123,45 en una tabla. En la tabla, la columna se define como un valor numérico o decimal, con una precisión de 5 y con la escala de 2.

El controlador ODBC que se usa para ejecutar este programa debe admitir la funcionalidad de ODBC 3.0.


``` C
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

void main() {

   SQLHENV    henv  = NULL;
   SQLHDBC    hdbc  = NULL;
   SQLHSTMT   hstmt = NULL;

   SQL_NUMERIC_STRUCT   NumStr;
   SQLINTEGER           cbNumStr = sizeof (NumStr);

   SQLAllocHandle(SQL_HANDLE_ENV, NULL, &henv);

   /* Set the ODBC behavior version. */ 
   SQLSetEnvAttr(henv,
         SQL_ATTR_ODBC_VERSION,
         (SQLPOINTER) SQL_OV_ODBC3,
         SQL_IS_INTEGER);

   SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);

   /* Substitute your own connection information */ 
   SQLConnect(hdbc,
      (SQLCHAR *) "MyDSN", 5,
      (SQLCHAR *) "UserID", 6,
      (SQLCHAR *) "Password", 8);

   SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);

   /*
      Set up the SQL_NUMERIC_STRUCT, NumStr, to hold "123.45".

      First, we need to scale 123.45 to an integer: 12345
      One way to switch the bytes is to convert 12345 to Hex:  0x3039
      Since the least significant byte will be stored starting from the
      leftmost byte, "0x3039" will be stored as "0x3930".

      The precision and scale fields are not used for input to the driver,
      only for output from the driver. The precision and scale will be set
      in the application parameter descriptor later.
   */ 

   NumStr.sign = 1;   /* 1 if positive, 2 if negative */ 

   memset (NumStr.val, 0, 16);
   NumStr.val [0] = 0x39;
   NumStr.val [1] = 0x30;

   /* SQLBindParameter needs to be called before SQLSetDescField */ 
   SQLBindParameter(hstmt,
          1,
          SQL_PARAM_INPUT,
          SQL_C_NUMERIC,
          SQL_NUMERIC,
          5,
          2,
          &NumStr,
          0,
          (SQLINTEGER *) &cbNumStr);

   /* Modify the fields in the implicit application parameter descriptor */ 
   SQLHDESC   hdesc = NULL;

   SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);
   SQLSetDescField(hdesc, 1, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_PRECISION, (SQLPOINTER) 5, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_SCALE, (SQLPOINTER) 2, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_DATA_PTR, (SQLPOINTER) &NumStr, 0);

   SQLExecDirect(hstmt,
         (SQLCHAR *) "INSERT INTO table (numeric_column) VALUES (?)",
         SQL_NTS);

   SQLFreeHandle(SQL_HANDLE_STMT, hstmt);

   SQLDisconnect (hdbc);

   SQLFreeHandle(SQL_HANDLE_DBC, hdbc);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
}
```


<!--
GeneMi historical notes, 2017/July/12. Per Jason.C

https://go.microsoft.com/fwlink/?LinkId=147596

https://support.microsoft.com/help/222831

https://web.archive.org/web/20140319133434/http:/support.microsoft.com:80/kb/222831

https://web.archive.org/web/20080505073901/http:/support.microsoft.com:80/kb/181254

https://docs.microsoft.com/sql/odbc/reference/appendixes/c-data-types
-->

