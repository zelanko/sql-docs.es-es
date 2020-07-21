---
title: Llamar a un procedimiento almacenado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- ODBC, stored procedures
- stored procedures [ODBC], calling
- SQL Server Native Client ODBC driver, stored procedures
- ODBC CALL escape sequence
- escape sequences [SQL Server]
- CALL statement
ms.assetid: d13737f4-f641-45bf-b56c-523e2ffc080f
author: rothja
ms.author: jroth
ms.openlocfilehash: c6fa704e45e4e85b479ae8a40a3e567bea1ec5e9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049719"
---
# <a name="calling-a-stored-procedure"></a>Llamar a un procedimiento almacenado
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite la secuencia de escape ODBC Call y la [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción [Execute](/sql/t-sql/language-elements/execute-transact-sql) para ejecutar procedimientos almacenados; la secuencia de escape ODBC Call es el método preferido. El uso de la sintaxis ODBC permite que una aplicación recupere los códigos de retorno de los procedimientos almacenados y el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client también está optimizado para usar un protocolo originalmente desarrollado para enviar llamadas a procedimiento remoto (RPC) entre equipos que ejecutan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este protocolo RPC aumenta el rendimiento eliminando gran parte del procesamiento de parámetros y análisis de instrucciones que se realiza en el servidor.  
  
> [!NOTE]  
>  Al llamar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimientos almacenados mediante parámetros con nombre con ODBC (para obtener más información, vea [enlazar parámetros por nombre (parámetros con nombre)](https://go.microsoft.com/fwlink/?LinkID=209721)), los nombres de los parámetros deben empezar por el \@ carácter ' '. Se trata de una restricción específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client exige esta restricción de una manera más estricta que Microsoft Data Access Components (MDAC).  
  
 La secuencia de escape ODBC CALL para llamar a un procedimiento es:  
  
 {[**? =**]**Call**_procedure_name_[([*parámetro*] [**,**[*parámetro*]]...)]}  
  
 donde *procedure_name* especifica el nombre de un procedimiento y un *parámetro* especifica un parámetro de procedimiento. Los parámetros con nombre solo se admiten en instrucciones que utilizan la secuencia de escape ODBC CALL.  
  
 Un procedimiento puede tener cero o más parámetros. También puede devolver un valor (que se indica con el marcador de parámetro opcional ?= al inicio de la sintaxis). Si un parámetro es de entrada o de entrada/salida, puede ser un literal o un marcador de parámetro. Si el parámetro es de salida, debe ser un marcador de parámetro porque se desconoce la salida. Los marcadores de parámetros se deben enlazar con [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) antes de que se ejecute la instrucción de llamada de procedimiento.  
  
 Los parámetros de entrada y de entrada/salida pueden omitirse de las llamadas a procedimiento. Si se llama a un procedimiento con paréntesis pero sin ningún parámetro, el controlador indica al origen de datos que use el valor predeterminado para el primer parámetro. Por ejemplo:  
  
 {**call** _procedure_name_**()**}  
  
 Si el procedimiento no tiene ningún parámetro, puede producirse un error en el procedimiento. Si se llama a un procedimiento sin paréntesis, el controlador no envía ningún valor de parámetro. Por ejemplo:  
  
 {**call** _procedure_name_}  
  
 Pueden especificarse literales para los parámetros de entrada y de entrada/salida en llamadas a procedimiento. Por ejemplo, el procedimiento InsertOrder tiene cinco parámetros de entrada. La siguiente llamada a InsertOrder omite el primer parámetro, proporciona un literal para el segundo parámetro y usa un marcador de parámetro para el tercero, cuarto y quinto parámetro. (Los parámetros se numeran secuencialmente, comenzando por el valor 1.)  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}  
```  
  
 Tenga en cuenta que aunque se omita un parámetro, la coma que lo separa de los demás parámetros debe estar presente. Si se omite un parámetro de entrada o de entrada/salida, el procedimiento usa el valor predeterminado del parámetro. Otras formas de especificar el valor predeterminado de un parámetro de entrada o de entrada/salida consisten en establecer el valor del búfer de longitud/indicador enlazado al parámetro en SQL_DEFAULT_PARAM, o bien, usar la palabra clave DEFAULT.  
  
 Si se omite un parámetro de entrada/salida, o si se proporciona un literal para el parámetro, el controlador descarta el valor de salida. Del mismo modo, si se omite el marcador de parámetro para el valor devuelto de un procedimiento, el controlador descarta dicho valor devuelto. Finalmente, si una aplicación especifica un parámetro de valor devuelto para un procedimiento que no devuelve ningún valor, el controlador establece el valor del búfer de longitud/indicador enlazado al parámetro en SQL_NULL_DATA.  
  
## <a name="delimiters-in-call-statements"></a>Delimitadores en instrucciones CALL  
 De forma predeterminada, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client también admite una opción de compatibilidad específica de la secuencia de escape ODBC { CALL }. El controlador acepta instrucciones CALL con un solo conjunto de comillas dobles que delimitan el nombre del procedimiento almacenado completo:  
  
```  
{ CALL "master.dbo.sp_who" }  
```  
  
 De forma predeterminada, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client también acepta instrucciones CALL que siguen las reglas ISO e incluyen cada identificador entre comillas dobles:  
  
```  
{ CALL "master"."dbo"."sp_who" }  
```  
  
 No obstante, cuando el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se ejecuta con la configuración predeterminada no admite el uso de cualquier forma de identificador entrecomillado con identificadores que contienen caracteres no especificados como legales en identificadores por el estándar ISO. Por ejemplo, el controlador no puede tener acceso a un procedimiento almacenado denominado **"My. proc"** mediante una instrucción call con identificadores entre comillas:  
  
```  
{ CALL "MyDB"."MyOwner"."My.Proc" }  
```  
  
 El controlador interpreta esta instrucción como:  
  
```  
{ CALL MyDB.MyOwner.My.Proc }  
```  
  
 El servidor genera un error que indica que no existe un servidor vinculado denominado **MyDB** .  
  
 Este problema no ocurre si se usan identificadores entre paréntesis; la instrucción se interpreta correctamente:  
  
```  
{ CALL [MyDB].[MyOwner].[My.Table] }  
```  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar procedimientos almacenados](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
