---
title: 'Ibcpsession:: Bcpcontrol (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPControl (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPControl method
ms.assetid: d58f3fe1-45e3-4e46-8e9c-000971829d99
caps.latest.revision: 50
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 703999be362bdaa9f26816da6edb386e38e62e0e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37432554"
---
# <a name="ibcpsessionbcpcontrol-ole-db"></a>IBCPSession::BCPControl (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Establece las opciones para una operación de copia masiva.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPControl(   
      int eOption,  
      void *iValue);  
```  
  
## <a name="remarks"></a>Notas  
 El **BCPControl** método establece varios parámetros de control para operaciones de copia masiva, incluido el número de errores permitidos antes de cancelar una copia masiva, los números de la primera y última fila para copiar desde un archivo de datos y el tamaño del lote.  
  
 Este método se utiliza también para especificar la instrucción SELECT que se utiliza en la copia masiva de datos desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede establecer el **eOption** argumento en BCP_OPTION_HINTS y **iValue** argumento tiene un puntero a una cadena de caracteres anchos que contiene la instrucción SELECT.  
  
 Los valores posibles de *eOption* son:  
  
|Opción|Descripción|  
|------------|-----------------|  
|BCP_OPTION_ABORT|Detiene una operación de copia masiva que ya está en curso. Puede llamar a la **BCPControl** método con un *eOption* argumento de BCP_OPTION_ABORT desde otro subproceso para detener una operación de copia masiva en ejecución. El *iValue* argumento se omite.|  
|BCP_OPTION_BATCH|El número de filas por lote. El valor predeterminado es 0, lo que indica que todas las filas de una tabla cuando se extraen los datos, o cuando se copian datos de los archivos de todas las filas de los datos de usuario [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un valor menor que 1 restablece BCP_OPTION_BATCH al valor predeterminado.|  
|BCP_OPTION_DELAYREADFMT|Un valor booleano, si establece en true, hará que [ibcpsession:: Bcpreadfmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) para leer en la ejecución. Si es false (valor predeterminado), ibcpsession:: Bcpreadfmt le inmediatamente leer el archivo de formato. Se producirá un error de secuencia si **BCP_OPTION_DELAYREADFMT** es true y se llama a ibcpsession:: BCPColumns o ibcpsession:: BCPColFmt.<br /><br /> También se producirá un error de secuencia si se llama a `IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)FALSE))` después de llamar a `IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)TRUE)` e ibcpsession:: Bcpwritefmt.<br /><br /> Para obtener más información, consulte [detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md).|  
|BCP_OPTION_FILECP|El *iValue* argumento contiene el número de la página de códigos del archivo de datos. Puede especificar el número de la página de códigos, como 1252 u 850, o uno de los valores siguientes:<br /><br /> BCP_FILECP_ACP: los datos del archivo están en la página de códigos de Microsoft Windows® del cliente.<br /><br /> BCP_FILECP_OEMCP: los datos del archivo están en la página de códigos OEM del cliente (valor predeterminado).<br /><br /> BCP_FILECP_RAW: los datos del archivo están en la página de códigos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|BCP_OPTION_FILEFMT|Número de versión del formato de archivo de datos. Puede ser 80 ([!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]), 90 ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]), 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]), 110 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) o 120 ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). 120 es el valor predeterminado. Esto resulta útil para exportar e importar datos en formatos admitidos en versiones anteriores del servidor.  Por ejemplo importar datos obtenidos de una columna de texto en un [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] server en un **varchar (max)** columna en un [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] servidor o posterior, debe especificar 80. De forma similar, si especifica 80 al exportar datos desde un **varchar (max)** columna, éstos se guardarán al igual que las columnas de texto se guardan en el [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] dar formato y se pueden importar a una columna de texto de un [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] server.|  
|BCP_OPTION_FIRST|La primera fila de datos del archivo o la tabla que se copia. El valor predeterminado es 1; un valor menor que 1 reinicializa esta opción a su valor predeterminado.|  
|BCP_OPTION_FIRSTEX|En operaciones de salida de BCP, especifica la primera fila de la tabla de base de datos que se copia en el archivo de datos.<br /><br /> En operaciones de entrada de BCP, especifica la primera fila del archivo de datos que se copia en la tabla de base de datos.<br /><br /> El *iValue* parámetro debe ser la dirección de un entero de 64 bits con signo que contiene el valor. El valor máximo que se puede pasar a BCPFIRSTEX es 2^63-1.|  
|BCP_OPTION_FMTXML|Se utiliza para especificar que el archivo de formato generado debe estar en un formato XML. Está apagado de forma predeterminada y de forma predeterminada los archivos de formato se guardan como archivos de texto. El formato de archivo XML proporciona mayor flexibilidad, pero con algunas restricciones más. Por ejemplo, no puede especificar el prefijo ni el terminador de un campo simultáneamente, lo que es posible en archivos de formatos anteriores.<br /><br /> Nota: Los archivos de formato XML sólo son compatibles cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramientas se instalan junto con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.|  
|BCP_OPTION_HINTS|El *iValue* argumento contiene un puntero de cadena de caracteres anchos. La cadena a la que apunta especifica sugerencias de procesamiento de copia masiva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que devuelve un conjunto de resultados. Si se especifica una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que devuelve más de un conjunto de resultados, se omiten todos los conjuntos de resultados posteriores al primero.|  
|BCP_OPTION_KEEPIDENTITY|Cuando el *iValue* argumento está establecido en TRUE, esta opción especifica que los métodos de copia masiva insertan valores de datos proporcionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las columnas definidas con una restricción de identidad. El archivo de entrada debe proporcionar valores para las columnas de identidad. Si no se establece, se generan nuevos valores de identidad para las filas insertadas. No se tiene en cuenta ningún dato presente en el archivo para las columnas de identidad.|  
|BCP_OPTION_KEEPNULLS|Especifica si los valores de datos vacíos del archivo se convertirán en valores NULL en la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando el *iValue* argumento está establecido en TRUE, los valores vacíos se convierten en NULL en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla. Con el valor predeterminado, los valores vacíos se convierten en un valor predeterminado para la columna en la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si existe un valor predeterminado.|  
|BCP_OPTION_LAST|La última fila que se copia. El valor predeterminado es copiar todas las filas. Un valor menor que 1 reinicia esta opción a su valor predeterminado.|  
|BCP_OPTION_LASTEX|En operaciones de salida de BCP, especifica la última fila de la tabla de base de datos que se copia en el archivo de datos.<br /><br /> En operaciones de entrada de BCP, especifica la última fila del archivo de datos que se copia en la tabla de base de datos.<br /><br /> El *iValue* parámetro debe ser la dirección de un entero de 64 bits con signo que contiene el valor. El valor máximo que se puede pasar a BCPLASTEX es 2^63-1.|  
|BCP_OPTION_MAXERRS|El número de errores permitido antes de que la operación de copia masiva genere un error. El valor predeterminado es 10. Un valor menor que 1 reinicia esta opción a su valor predeterminado. La copia masiva impone un máximo de 65.535 errores. Si se intenta establecer esta opción en un valor mayor que 65.535, la opción se establece en 65.535.|  
|BCP_OPTION_ROWCOUNT|Devuelve el número de filas afectado por la operación actual (o última) de BCP.|  
|BCP_OPTION_TEXTFILE|El archivo de datos no es un archivo binario, sino un archivo de texto. BCP detecta si el archivo de texto es Unicode o no comprobando el marcador de byte Unicode en los primeros 2 bytes del archivo de datos.|  
|BCP_OPTION_UNICODEFILE|Cuando se establece en TRUE, esta opción especifica que el archivo de entrada es un formato de archivo de Unicode.|  
  
## <a name="arguments"></a>Argumentos  
 *eOption*[in]  
 Establézcalo en una de las opciones de la lista de la sección anterior de notas.  
  
 *iValue*[in]  
 El valor para el elemento especificado *eOption*. El *iValue* argumento es un valor entero en un puntero void para permitir la ampliación futura a valores de 64 bits.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor; Para obtener información detallada, use el [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) interfaz.  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, el [ibcpsession:: BCPInit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) no se llamó al método antes de llamar a esta función.  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
## <a name="see-also"></a>Vea también  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
