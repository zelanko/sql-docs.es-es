---
title: Convertir de DB-Library a ODBC de copia masiva | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- converting DB-Library to ODBC bulk copy
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], DB-Library bulk copy
- ODBC, bulk copy operations
- DB-Library bulk copy
ms.assetid: 0bc15bdb-f19f-4537-ac6c-f249f42cf07f
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bc8072a1bd0f0e3a097a01696c9d034e0acb33c7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32946310"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>Convertir un programa de copia masiva de DB-Library a ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Convertir un programa de copia masiva de DB-Library a ODBC es fácil, ya que la mayor parte copiar las funciones admitidas por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client son similares a las funciones de copia masiva de DB-Library, con las siguientes excepciones:  
  
-   Las aplicaciones DB-Library pasan un puntero a una estructura DBPROCESS como primer parámetro de las funciones de copia masiva. En las aplicaciones ODBC, el puntero a DBPROCESS se reemplaza por un identificador de conexión ODBC.  
  
-   Llamada a las aplicaciones de DB-Library **BCP_SETL** antes de conectarse para habilitar las operaciones de copia masiva en DBPROCESS. Las aplicaciones ODBC en su lugar, llame a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) antes de conectarse para habilitar las operaciones de forma masiva en un identificador de conexión:  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client no admite controladores de mensajes y errores de DB-Library; se debe llamar a **SQLGetDiagRec** obtener errores y mensajes generados por las funciones de copia masiva ODBC. Las versiones ODBC de las funciones de copia masiva devuelven los códigos de retorno de copia masiva estándar, es decir, SUCCEED o FAILED, no códigos de retorno de estilo ODBC, como SQL_SUCCESS o SQL_ERROR.  
  
-   Los valores especificados para DB-Library [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen* parámetro se interpretan de forma distinta a ODBC **bcp_bind *** cbData* parámetro.  
  
    |Condición indicada|DB-Library *varlen* valor|ODBC *cbData* valor|  
    |-------------------------|--------------------------------|-------------------------|  
    |Se suministraron valores NULL|0|-1 (SQL_NULL_DATA)|  
    |Se suministraron datos variables|-1|-10 (SQL_VARLEN_DATA)|  
    |Cadena binaria o carácter de longitud cero|N/D|0|  
  
     En DB-Library, un *varlen* valor -1 indica que se han suministrado datos de longitud variable, que en el archivo ODBC *cbData* se interpreta que solo los valores NULL no se ha proporcionado. Cambiar cualquier DB-Library *varlen* especificaciones de -1 a SQL_VARLEN_DATA y *varlen* especificaciones de 0 a SQL_NULL_DATA.  
  
-   DB-Library  **bcp_colfmt *** file_collen* y ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)* cbUserData * tienen el mismo problema que el **bcp_bind *** varlen*y *cbData* parámetros indican anteriormente. Cambiar cualquier DB-Library *file_collen* especificaciones de -1 a SQL_VARLEN_DATA y *file_collen* especificaciones de 0 a SQL_NULL_DATA.  
  
-   El *iValue* parámetro de ODBC [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) función es un puntero void. En DB-Library, *iValue* era un entero. Convertir los valores con ODBC *iValue* a void *.  
  
-   El **bcp_control** opción BCPMAXERRS especifica cuántas filas individuales pueden tener errores antes de que se produce un error en una operación de copia masiva. El valor predeterminado para BCPMAXERRS es 0 (error en el primer error) en la versión de DB-Library de **bcp_control** y 10 en la versión de ODBC. Aplicaciones de DB-Library que dependen del valor predeterminado de 0 para finalizar una operación de copia masiva deben modificarse para llamar a ODBC **bcp_control** establecer BCPMAXERRS en 0.  
  
-   ODBC **bcp_control** función admite las siguientes opciones no compatibles con la versión de DB-Library de **bcp_control**:  
  
    -   BCPODBC  
  
         Cuando se establece en TRUE, especifica que **datetime** y **smalldatetime** valores guardados en el formato de caracteres tendrán el prefijo de la secuencia de escape ODBC marca de tiempo y el sufijo. Esto solo se aplica a las operaciones BCP_OUT.  
  
         Con BCPODBC establecido en FALSE, una **datetime** valor convertido en una cadena de caracteres se genera como:  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         Con BCPODBC establecido en TRUE, el mismo **datetime** valor se genera como:  
  
        ```  
        {ts '1997-01-01 00:00:00.000' }  
        ```  
  
    -   BCPKEEPIDENTITY  
  
         Cuando se establece en TRUE, especifica que las funciones de copia masiva deben insertar valores de datos suministrados para las columnas con restricciones de identidad. Si no se establece, se generan nuevos valores de identidad para las filas insertadas.  
  
    -   BCPHINTS  
  
         Especifica diversas optimizaciones de copia masiva. Esta opción no puede usarse en la versión 6.5 ni en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   BCPFILECP  
  
         Especifica la página de códigos del archivo de copia masiva.  
  
    -   BCPUNICODEFILE  
  
         Especifica que un archivo de copia masiva en modo de carácter es un archivo Unicode.  
  
-   ODBC **bcp_colfmt** función no admite la *file_type* indicador de SQLCHAR porque entra en conflicto con la definición de tipo de SQLCHAR de ODBC. Utilice en su lugar SQLCHARACTER para **bcp_colfmt**.  
  
-   En las versiones ODBC de funciones de copia masiva, el formato para trabajar con **datetime** y **smalldatetime** valores en cadenas de caracteres es el formato aaaa-mm-dd SSS; **smalldatetime** valores utilizan el formato aaaa-mm-dd hh.  
  
     La versión de DB-Library de las funciones de copia masiva aceptan **datetime** y **smalldatetime** valores en cadenas de caracteres con varios formatos:  
  
    -   El formato predeterminado es *mmm dd aaaa hh: mmXX* donde *xx* es AM o PM.  
  
    -   **fecha y hora** y **smalldatetime** cadenas en cualquier formato admitido por la biblioteca de base de datos de caracteres **dbconvert** función.  
  
    -   Cuando el **usar configuración internacional** casilla está activada en DB-Library **opciones** pestaña de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramienta de red del cliente, las funciones de copia masiva de DB-Library también aceptan las fechas en la configuración regional formato de fecha definido para la configuración regional del registro del equipo cliente.  
  
     Las funciones de copia masiva de DB-Library no aceptan ODBC **datetime** y **smalldatetime** formatos.  
  
     Si el atributo SQL_SOPT_SS_REGIONALIZE de la instrucción está establecido en SQL_RE_ON, las funciones de copia masiva de ODBC aceptan fechas en el formato de fecha regional definido para la configuración regional del Registro del equipo cliente.  
  
-   Al generar **dinero** valores en el formato de caracteres, ODBC masiva copia funciones proporcionan cuatro dígitos de precisión y ningún separador de millares; Versiones de DB-Library solo proporcionan dos dígitos de precisión e incluyen los separadores de millares.  
  
## <a name="see-also"></a>Vea también  
 [Realizar operaciones de copia masiva &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
