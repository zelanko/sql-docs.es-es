---
title: Llamar a un procedimiento almacenado (OLE DB) | Documentos de Microsoft
description: Llamar a un procedimiento almacenado (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- RPC escape sequence
- OLE DB, stored procedures
- parameters [OLE DB Driver for SQL Server], OLE DB
- ODBC CALL escape sequence
- stored procedures [OLE DB], calling
- OLE DB Driver for SQL Server, stored procedures
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 1dae3bfeae19e302d7e6320dcd61695d5d79d1e1
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612290"
---
# <a name="stored-procedures---calling"></a>Procedimientos almacenados - llamada
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Un procedimiento almacenado puede tener cero o más parámetros. También puede devolver un valor. Cuando se usa el controlador OLE DB para SQL Server, se pueden pasar parámetros a un procedimiento almacenado:  
  
-   Codificando de forma rígida el valor de datos.  
  
-   Utilizando un marcador de parámetro (?) para especificar parámetros, enlazar una variable de programa al marcador de parámetro y, a continuación, colocar el valor de datos en la variable de programa.  
  
> [!NOTE]  
>  Cuando se llama a procedimientos almacenados de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando parámetros con nombre con OLE DB, los nombres de parámetro deben empezar con el carácter '@'. Se trata de una restricción específica de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El controlador OLE DB para SQL Server exige esta restricción de forma más estricta que MDAC.  
  
 Para admitir los parámetros, el **ICommandWithParameters** interfaz se expone en el objeto de comando. Para utilizar parámetros, el consumidor describe primero los parámetros al proveedor mediante una llamada a la **ICommandWithParameters:: SetParameterInfo** método (u opcionalmente prepara una instrucción de llamada que llama el **GetParameterInfo** método). A continuación, el consumidor crea un descriptor de acceso que especifica la estructura de un búfer y coloca los valores de parámetro en este búfer. Por último, pasa el identificador de descriptor de acceso y un puntero al búfer para **Execute**. En las llamadas posteriores a **Execute**, el consumidor coloca nuevos valores de parámetro en el búfer y llama **Execute** con el puntero de búfer y de identificador de descriptor de acceso.  
  
 En primer lugar debe llamar un comando que llama a un procedimiento almacenado temporal utilizando parámetros **ICommandWithParameters:: SetParameterInfo** para definir la información de parámetros, antes de que el comando se puede preparar correctamente. Esto es porque el nombre interno para un procedimiento almacenado temporal difiere del nombre externo utilizado por un cliente y MSOLEDBSQL no pueden consultar las tablas del sistema para determinar la información de parámetros para un procedimiento almacenado temporal.  
  
 Estos son los pasos en el proceso de enlace de parámetro:  
  
1.  Rellene la información de parámetros en una matriz de estructuras DBPARAMBINDINFO; es decir, el nombre del parámetro, el nombre específico del proveedor para el tipo de datos del parámetro o un nombre del tipo de datos estándar, etc. Cada estructura de la matriz describe un parámetro. Esta matriz, a continuación, se pasa a la **SetParameterInfo** método.  
  
2.  Llame a la **ICommandWithParameters:: SetParameterInfo** método para describir los parámetros al proveedor. **SetParameterInfo** especifica el tipo de datos nativos de cada parámetro. **SetParameterInfo** argumentos son:  
  
    -   El número de parámetros para los que se ha de establecer información de tipo.  
  
    -   Una matriz de ordinales de parámetros para los que se ha de establecer información de tipo.  
  
    -   Una matriz de estructuras DBPARAMBINDINFO.  
  
3.  Crear un descriptor de acceso de parámetro mediante el **IAccessor:: CreateAccessor** comando. El descriptor de acceso especifica la estructura de un búfer y coloca los valores de parámetro en el búfer. El **CreateAccessor** comando crea un descriptor de acceso de un conjunto de enlaces. El consumidor describe estos enlaces utilizando una matriz de estructuras DBBINDING. Cada enlace asocia un parámetro único al búfer del consumidor y contiene información como:  
  
    -   El ordinal del parámetro al que se aplica el enlace.  
  
    -   Lo que se enlaza (el valor de datos, su longitud y su estado).  
  
    -   El desplazamiento en el búfer a cada una de estas partes.  
  
    -   La longitud y el tipo del valor de datos tal y como está en el búfer del consumidor.  
  
     Un descriptor de acceso queda identificado por su identificador, que es de tipo HACCESSOR. Este identificador es devuelto por la **CreateAccessor** método. Cada vez que el consumidor termina de utilizar un descriptor de acceso, el consumidor debe llamar a la **ReleaseAccessor** método para liberar la memoria que utiliza.  
  
     Cuando el consumidor llama a un método, como **ICommand:: Execute**, pasa el identificador a un descriptor de acceso y un puntero al propio búfer. El proveedor utiliza este descriptor de acceso para determinar cómo transferir los datos incluidos en el búfer.  
  
4.  Rellene la estructura DBPARAMS. Las variables de consumidor de qué parámetro de entrada se toman los valores y en qué parámetro de salida se escriben los valores se pasan en tiempo de ejecución para **ICommand:: Execute** en la estructura DBPARAMS. La estructura DBPARAMS incluye tres elementos:  
  
    -   Un puntero al búfer del que el proveedor recupera los datos de parámetro de entrada y al que devuelve los datos de parámetro de salida, de acuerdo con los enlaces especificados por el identificador de descriptor de acceso.  
  
    -   El número de conjuntos de parámetros que hay en el búfer.  
  
    -   El identificador de descriptor de acceso creado en el paso 3.  
  
5.  Ejecute el comando mediante el uso de **ICommand:: Execute**.  
  
## <a name="methods-of-calling-a-stored-procedure"></a>Métodos para llamar a un procedimiento almacenado  
 Al ejecutar un procedimiento almacenado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el controlador OLE DB para SQL Server admite el:  
  
-   Secuencia de escape ODBC CALL.  
  
-   Secuencia de escape RPC (llamada a procedimiento remoto).  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] Instrucción EXECUTE.   
  
### <a name="odbc-call-escape-sequence"></a>Secuencia de escape ODBC CALL  
 Si conoce la información de parámetros, llame a **ICommandWithParameters:: SetParameterInfo** método para describir los parámetros al proveedor. De lo contrario, cuando se utiliza la sintaxis ODBC CALL para llamar a un procedimiento almacenado, el proveedor llama a una función auxiliar para buscar la información de parámetros del procedimiento almacenado.  
  
 Si no está seguro de la información de parámetros (metadatos de parámetros), es preferible utilizar la sintaxis ODBC CALL.  
  
 La sintaxis general para llamar a un procedimiento utilizando la secuencia de escape ODBC CALL es la siguiente:  
  
 {[**? =**]**llamada ***nombre_procedimiento*[**(**[*parámetro*] [**,**[*parámetro*]]...** )**]}  
  
 Por ejemplo:  
  
```  
{call SalesByCategory('Produce', '1995')}  
```  
  
### <a name="rpc-escape-sequence"></a>Secuencia de escape RPC  
 La secuencia de escape RPC es similar a la sintaxis ODBC CALL para llamar a un procedimiento almacenado. Si va a llamar al procedimiento varias veces, la secuencia de escape RPC es la que proporciona el rendimiento óptimo de entre los tres métodos existentes para llamar a un procedimiento almacenado.  
  
 Cuando se utiliza la secuencia de escape RPC para ejecutar un procedimiento almacenado, el proveedor no llama a ninguna función auxiliar para determinar la información de parámetros (como hace en el caso de la sintaxis ODBC CALL). La sintaxis RPC es más sencilla que la sintaxis ODBC CALL, por lo que el comando se analiza con mayor rapidez y se mejora el rendimiento. En este caso, debe proporcionar la información de parámetros mediante la ejecución de **ICommandWithParameters:: SetParameterInfo**.  
  
 La secuencia de escape RPC exige que tenga un valor devuelto. Si el procedimiento almacenado no devuelve un valor, el servidor devuelve de forma predeterminada un 0. Además, no puede abrir un cursor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el procedimiento almacenado. El procedimiento almacenado se prepara implícitamente y la llamada a **ICommandPrepare:: Prepare** se producirá un error. Debido a la incapacidad para preparar una llamada RPC, no puede consultar los metadatos de columna; IColumnsInfo:: GetColumnInfo e IColumnsRowset:: GetColumnsRowset devolverán DB_E_NOTPREPARED.  
  
 Si conoce todos los metadatos de parámetros, la secuencia de escape RPC es la opción recomendada para ejecutar los procedimientos almacenados.  
  
 Este es un ejemplo de secuencia de escape RPC para llamar a un procedimiento almacenado:  
  
```  
{rpc SalesByCategory}  
```  
  
 Para una aplicación de ejemplo que muestra una secuencia de escape RPC, vea [ejecutar un procedimiento almacenado &#40;mediante la sintaxis RPC&#41; y proceso de códigos de retorno y parámetros de salida &#40;OLE DB&#41;](../../oledb/ole-db-how-to/results/execute-stored-procedure-with-rpc-and-process-output.md).  
  
### <a name="transact-sql-execute-statement"></a>Instrucción EXECUTE de Transact-SQL:  
 La secuencia de escape ODBC CALL y la secuencia de escape RPC son los métodos preferidos para llamar a un procedimiento almacenado en lugar de la [EXECUTE](../../../t-sql/language-elements/execute-transact-sql.md) instrucción. El controlador OLE DB para SQL Server utiliza el mecanismo RPC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para optimizar el procesamiento de comandos. Este protocolo RPC aumenta el rendimiento eliminando gran parte del procesamiento de parámetros y análisis de instrucciones que se realiza en el servidor.  
  
 Este es un ejemplo de la [!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE** instrucción:  
  
```  
EXECUTE SalesByCategory 'Produce', '1995'  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados](../../oledb/ole-db/stored-procedures.md)  
  
  
