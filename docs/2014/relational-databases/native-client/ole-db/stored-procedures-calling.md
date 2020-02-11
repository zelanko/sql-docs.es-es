---
title: Llamar a un procedimiento almacenado (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- RPC escape sequence
- OLE DB, stored procedures
- parameters [SQL Server Native Client], OLE DB
- ODBC CALL escape sequence
- stored procedures [OLE DB], calling
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: 8e5738e5-4bbe-4f34-bd69-0c0633290bdd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7385dddea48813615a851979e526af5f03a23332
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68206581"
---
# <a name="calling-a-stored-procedure-ole-db"></a>Llamar a un procedimiento almacenado (OLE DB)
  Un procedimiento almacenado puede tener cero o más parámetros. También puede devolver un valor. Cuando se usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] el proveedor de OLE DB de Native Client, se pueden pasar los parámetros a un procedimiento almacenado:  
  
-   Codificando de forma rígida el valor de datos.  
  
-   Utilizando un marcador de parámetro (?) para especificar parámetros, enlazar una variable de programa al marcador de parámetro y, a continuación, colocar el valor de datos en la variable de programa.  
  
> [!NOTE]  
>  Cuando se llama a procedimientos almacenados de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante parámetros con nombre con OLE DB, los nombres de parámetro deben empezar con el carácter '\@'. Se trata de una restricción específica de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client aplica esta restricción de forma más estricta que MDAC.  
  
 Para admitir parámetros, se expone la interfaz **ICommandWithParameters** en el objeto de comando. Para usar parámetros, el cliente primero describe los parámetros al proveedor mediante una llamada al método **ICommandWithParameters::SetParameterInfo** (u opcionalmente prepara una instrucción de llamada que llama al método **GetParameterInfo**). A continuación, el consumidor crea un descriptor de acceso que especifica la estructura de un búfer y coloca los valores de parámetro en este búfer. Por último, pasa el identificador del descriptor de acceso y un puntero al búfer a **Execute**. En las llamadas posteriores a **Execute**, el cliente coloca nuevos valores de parámetro en el búfer y llama a **Execute** con el identificador del descriptor de acceso y el puntero al búfer.  
  
 Un comando que llama a un procedimiento almacenado temporal mediante parámetros, primero debe llamar a **ICommandWithParameters::SetParameterInfo** para definir la información de parámetros antes de que se pueda preparar el comando correctamente. Esto se debe a que el nombre interno para un procedimiento almacenado temporal difiere del nombre externo utilizado por un cliente y SQLOLEDB no puede consultar las tablas del sistema para determinar la información de parámetros para un procedimiento almacenado temporal.  
  
 Estos son los pasos en el proceso de enlace de parámetro:  
  
1.  Rellene la información de parámetros en una matriz de estructuras DBPARAMBINDINFO; es decir, el nombre del parámetro, el nombre específico del proveedor para el tipo de datos del parámetro o un nombre del tipo de datos estándar, etc. Cada estructura de la matriz describe un parámetro. Luego esta matriz se pasa al método **SetParameterInfo**.  
  
2.  Llame al método **ICommandWithParameters::SetParameterInfo** para describir los parámetros al proveedor. **SetParameterInfo** especifica el tipo de datos nativo de cada parámetro. Los argumentos de **SetParameterInfo** son:  
  
    -   El número de parámetros para los que se ha de establecer información de tipo.  
  
    -   Una matriz de ordinales de parámetros para los que se ha de establecer información de tipo.  
  
    -   Una matriz de estructuras DBPARAMBINDINFO.  
  
3.  Cree un descriptor de acceso a parámetros mediante el comando **IAccessor::CreateAccessor**. El descriptor de acceso especifica la estructura de un búfer y coloca los valores de parámetro en el búfer. El comando **CreateAccessor** crea un descriptor de acceso a partir de un conjunto de enlaces. El consumidor describe estos enlaces utilizando una matriz de estructuras DBBINDING. Cada enlace asocia un parámetro único al búfer del consumidor y contiene información como:  
  
    -   El ordinal del parámetro al que se aplica el enlace.  
  
    -   Lo que se enlaza (el valor de datos, su longitud y su estado).  
  
    -   El desplazamiento en el búfer a cada una de estas partes.  
  
    -   La longitud y el tipo del valor de datos tal y como está en el búfer del consumidor.  
  
     Un descriptor de acceso queda identificado por su identificador, que es de tipo HACCESSOR. El método **CreateAccessor** devuelve este identificador. Cada vez que el cliente termina de usar un descriptor de acceso, debe llamar al método **ReleaseAccessor** para liberar la memoria que retiene.  
  
     Cuando el cliente llama a un método, como **ICommand::Execute**, pasa automáticamente el identificador a un descriptor de acceso y un puntero a un búfer. El proveedor utiliza este descriptor de acceso para determinar cómo transferir los datos incluidos en el búfer.  
  
4.  Rellene la estructura DBPARAMS. Las variables del cliente de las que se toman los valores de parámetro de entrada y en las que se escriben los valores de parámetro de salida se pasan en tiempo de ejecución a **ICommand::Execute** en la estructura DBPARAMS. La estructura DBPARAMS incluye tres elementos:  
  
    -   Un puntero al búfer del que el proveedor recupera los datos de parámetro de entrada y al que devuelve los datos de parámetro de salida, de acuerdo con los enlaces especificados por el identificador de descriptor de acceso.  
  
    -   El número de conjuntos de parámetros que hay en el búfer.  
  
    -   El identificador de descriptor de acceso creado en el paso 3.  
  
5.  Ejecute el comando mediante **ICommand::Execute**.  
  
## <a name="methods-of-calling-a-stored-procedure"></a>Métodos para llamar a un procedimiento almacenado  
 Al ejecutar un procedimiento almacenado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite:  
  
-   Secuencia de escape ODBC CALL.  
  
-   Secuencia de escape RPC (llamada a procedimiento remoto).  
  
-   
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] Instrucción EXECUTE.   
  
### <a name="odbc-call-escape-sequence"></a>Secuencia de escape ODBC CALL  
 Si conoce la información de parámetros, llame al método **ICommandWithParameters::SetParameterInfo** para describir los parámetros al proveedor. De lo contrario, cuando se utiliza la sintaxis ODBC CALL para llamar a un procedimiento almacenado, el proveedor llama a una función del asistente para buscar la información de parámetros del procedimiento almacenado.  
  
 Si no está seguro de la información de parámetros (metadatos de parámetros), es preferible utilizar la sintaxis ODBC CALL.  
  
 La sintaxis general para llamar a un procedimiento utilizando la secuencia de escape ODBC CALL es la siguiente:  
  
 {[**? =**]**Call**_procedure_name_[**(**[*parámetro*] [**,**[*parámetro*]]... **)**]}  
  
 Por ejemplo:  
  
```  
{call SalesByCategory('Produce', '1995')}  
```  
  
### <a name="rpc-escape-sequence"></a>Secuencia de escape RPC  
 La secuencia de escape RPC es similar a la sintaxis ODBC CALL para llamar a un procedimiento almacenado. Si va a llamar al procedimiento varias veces, la secuencia de escape RPC es la que proporciona el rendimiento óptimo de entre los tres métodos existentes para llamar a un procedimiento almacenado.  
  
 Cuando se utiliza la secuencia de escape RPC para ejecutar un procedimiento almacenado, el proveedor no llama a ninguna función del asistente para determinar la información de parámetros (como hace en el caso de la sintaxis ODBC CALL). La sintaxis RPC es más sencilla que la sintaxis ODBC CALL, por lo que el comando se analiza con mayor rapidez y se mejora el rendimiento. En este caso, necesita proporcionar la información de parámetros mediante la ejecución de **ICommandWithParameters::SetParameterInfo**.  
  
 La secuencia de escape RPC exige que tenga un valor devuelto. Si el procedimiento almacenado no devuelve un valor, el servidor devuelve de forma predeterminada un 0. Además, no puede abrir un cursor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el procedimiento almacenado. El procedimiento almacenado se prepara de forma implícita y la llamada a **ICommandPrepare::Prepare** produce un error. Como no se puede preparar una llamada RPC, no se puede realizar una consulta en los metadatos de columna; IColumnsInfo::GetColumnInfo e IColumnsRowset::GetColumnsRowset devolverán DB_E_NOTPREPARED.  
  
 Si conoce todos los metadatos de parámetros, la secuencia de escape RPC es la opción recomendada para ejecutar los procedimientos almacenados.  
  
 Este es un ejemplo de secuencia de escape RPC para llamar a un procedimiento almacenado:  
  
```  
{rpc SalesByCategory}  
```  
  
 Para obtener una aplicación de ejemplo que muestra una secuencia de escape RPC, vea [ejecutar un procedimiento almacenado &#40;usar la sintaxis rpc&#41; y procesar códigos de retorno y parámetros de salida &#40;OLE DB&#41;](../../native-client-ole-db-how-to/results/execute-stored-procedure-with-rpc-and-process-output.md).  
  
### <a name="transact-sql-execute-statement"></a>Instrucción EXECUTE de Transact-SQL:  
 Las secuencias de escape ODBC CALL y RPC son los métodos preferidos para llamar a un procedimiento almacenado en lugar de la instrucción [EXECUTE](/sql/t-sql/language-elements/execute-transact-sql). El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client utiliza el mecanismo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] RPC de para optimizar el procesamiento de comandos. Este protocolo RPC aumenta el rendimiento eliminando gran parte del procesamiento de parámetros y análisis de instrucciones que se realiza en el servidor.  
  
 Este es un ejemplo de la instrucción EXECUTE[!INCLUDE[tsql](../../../includes/tsql-md.md)] ** de **:  
  
```  
EXECUTE SalesByCategory 'Produce', '1995'  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados](stored-procedures.md)  
  
  
