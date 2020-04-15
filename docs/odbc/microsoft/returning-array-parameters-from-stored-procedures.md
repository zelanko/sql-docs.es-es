---
title: Devolviendo los parámetros de la matriz de los procedimientos almacenados Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 2018069b-da5d-4cee-a971-991897d4f7b5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc998dadc0e0c4a4bfe054bfd1d40296bc176393
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292865"
---
# <a name="returning-array-parameters-from-stored-procedures"></a>Devolver los parámetros de matriz de los procedimientos almacenados
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 En Oracle 7.3, no hay forma de acceder a un tipo de registro PL/SQL excepto desde un programa PL/SQL. Si un procedimiento o función empaquetado tiene un argumento formal definido como un tipo de registro PL/SQL, no es posible enlazar ese argumento formal como parámetro. Utilice el tipo PL/SQL TABLE en el controlador ODBC de Microsoft para Oracle para invocar parámetros de matriz de procedimientos que contienen las secuencias de escape correctas.  
  
 Para invocar el procedimiento, utilice la sintaxis siguiente:  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  El \<parámetro de> max-records-requested debe ser mayor o igual que el número de filas presentes en el conjunto de resultados. De lo contrario, Oracle devuelve un error que el controlador pasa al usuario.  
>   
>  Los registros PL/SQL no se pueden utilizar como parámetros de matriz. Cada parámetro de matriz solo puede representar una columna de una tabla de base de datos.  
  
 En el ejemplo siguiente se define un paquete que contiene dos procedimientos que devuelven conjuntos de resultados diferentes y, a continuación, proporciona dos maneras de devolver conjuntos de resultados del paquete.  
  
## <a name="package-definition"></a>Definición del paquete:  
  
```  
CREATE OR REPLACE PACKAGE SimplePackage AS  
  
TYPE t_id is TABLE of  NUMBER(5)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Course is TABLE of VARCHAR2(10)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Dept is TABLE of VARCHAR2(5)  
    INDEX BY BINARY_INTEGER;  
  
PROCEDURE proc1  
   (  
   o_id             OUT    t_id,  
   ao_course       OUT    t_Course,  
   ao_dept         OUT    t_Dept  
   );  
  
TYPE t_pk1Type1 IS TABLE OF VARCHAR2(100) INDEX BY BINARY_INTEGER;  
TYPE t_pk1Type2 IS TABLE OF NUMBER INDEX BY BINARY_INTEGER;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   );  
  
END SimplePackage;  
  
CREATE OR REPLACE PACKAGE BODY SimplePackage AS  
    PROCEDURE  proc1 ( o_id OUT t_id,  
    ao_course OUT t_Course, ao_dept OUT t_Dept   ) AS  
    BEGIN  
          o_id(1):= 200;  
          ao_course(1) :=  'M101';  
          ao_dept(1) :=  'EEE' ;  
  
          o_id(2) := 201;  
          ao_course(2) :=  'PHY320';  
          ao_dept(2) :=  'ECE' ;  
  
     END proc1;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   )  
AS  
   i   NUMBER;  
BEGIN  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg2(i) := 'Row Number ' || to_char(i);  
   END LOOP;  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg3(i) := i;  
   END LOOP;  
END proc2;  
END SimplePackage;  
```  
  
#### <a name="to-invoke-procedure-proc1"></a>Para invocar el procedimiento PROC1  
  
1.  Devuelve todas las columnas de un único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  Devuelve cada columna como un único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     Esto devuelve tres conjuntos de resultados, uno para cada columna.  
  
#### <a name="to-invoke-procedure-proc2"></a>Para invocar el procedimiento PROC2  
  
1.  Devuelve todas las columnas de un único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  Devuelve cada columna como un único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 Asegúrese de que las aplicaciones capturan todos los conjuntos de resultados mediante la API [SQLMoreResults.](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) Para obtener más información, consulte la *referencia del programador ODBC*.  
  
> [!NOTE]  
>  En el controlador ODBC para Oracle versión 2.0, las funciones de Oracle que devuelven matrices PL/SQL no se pueden utilizar para devolver conjuntos de resultados.
