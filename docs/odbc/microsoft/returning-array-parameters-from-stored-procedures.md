---
title: Devolver los parámetros de matriz de los procedimientos almacenados | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a154a8739438b76f12e311d0dec0e9d98d886457
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127997"
---
# <a name="returning-array-parameters-from-stored-procedures"></a>Devolver los parámetros de matriz de los procedimientos almacenados
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 En Oracle 7.3, no hay ninguna manera de obtener acceso a un tipo de registro de PL/SQL, excepto de un programa de PL/SQL. Si un procedimiento empaquetada o una función tiene un argumento formal que se define como un tipo de registro de PL/SQL, no es posible enlazar ese argumento formal como un parámetro. Utilice el tipo de tabla de PL/SQL en el controlador ODBC de Microsoft para Oracle para invocar los parámetros de matriz de los procedimientos que contiene las secuencias de escape correctos.  
  
 Para invocar el procedimiento, use la sintaxis siguiente:  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  El \<solicitadas por los registros max > parámetro debe ser mayor o igual que el número de filas existentes en el conjunto de resultados. En caso contrario, Oracle devuelve un error que se pasa al usuario por el controlador.  
>   
>  Registros de PL/SQL no se puede usar como parámetros de matriz. Cada parámetro de matriz puede representar solo una columna de una tabla de base de datos.  
  
 El ejemplo siguiente define un paquete que contiene dos procedimientos que devuelven distintos conjuntos de resultados y, a continuación, proporciona dos maneras de devolver conjuntos de resultados del paquete.  
  
## <a name="package-definition"></a>Definición de paquete:  
  
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
  
1.  Devolver todas las columnas en un único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  Cada columna se devuelven como un único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     Esto devuelve tres conjuntos de resultados, una para cada columna.  
  
#### <a name="to-invoke-procedure-proc2"></a>Para invocar el procedimiento PROC2  
  
1.  Devolver todas las columnas en un único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  Cada columna se devuelven como un único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 Asegúrese de que las aplicaciones obtener todos los conjuntos de resultados utilizando la [SQLMoreResults](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) API. Para obtener más información, consulte el *referencia del programador de ODBC*.  
  
> [!NOTE]  
>  En el controlador ODBC para Oracle versión 2.0, las funciones de Oracle que devuelven matrices de PL/SQL no se puede usar para devolver conjuntos de resultados.
