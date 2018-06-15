---
title: 'Ibcpsession:: BCPInit (OLE DB) | Documentos de Microsoft'
description: IBCPSession::BCPInit (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPInit (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPInit method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 950e74338c441d773dace08689644d9bab5658ab
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35306014"
---
# <a name="ibcpsessionbcpinit-ole-db"></a>IBCPSession::BCPInit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Inicializa la estructura de copia masiva, realiza algunas comprobaciones de errores, comprueba que los datos y los nombres de archivo de formato son correctos y, a continuación, los abre.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPInit(   
      const wchar_t *pwszTable,  
      const wchar_t *pwszDataFile,  
      const wchar_t *pwszErrorFile,  
      int eDirection);  
```  
  
## <a name="remarks"></a>Notas  
 El **BCPInit** método debe llamarse antes que cualquier otro método de copia masiva. El **BCPInit** método realiza las inicializaciones necesarias para una copia masiva de datos entre la estación de trabajo y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 El **BCPInit** método examina la estructura de la tabla base de datos origen o destino, no el archivo de datos. Especifica los valores de formato de datos del archivo de datos basándose en cada columna de la tabla de base de datos, la vista o el conjunto de resultados de la instrucción SELECT. Esta especificación incluye el tipo de datos de cada columna, la presencia o ausencia de cadenas de bytes de un indicador de longitud o nulo y de terminador en los datos, y el ancho de los tipos de datos de longitud fija. El **BCPInit** método establece estos valores como se indica a continuación:  
  
-   El tipo de datos especificado es el tipo de datos de la columna de la tabla de base de datos, la vista o el conjunto de resultados de una instrucción SELECT. El tipo de datos es enumerado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos nativos especificados en el controlador OLE DB para el archivo de encabezado de SQL Server (msoledbsql.h). Sus valores están en el modelo de BCP_TYPE_XXX. Los datos están representados en el formato del equipo. Es decir, los datos de una columna de tipo de datos entero están representados por una secuencia de cuatro bytes "big endian" o "little endian" basada en el equipo que creó el archivo de datos.  
  
-   Si un tipo de datos de base de datos es de longitud fija, los datos del archivo de datos también serán de longitud fija. Métodos de copia masiva que procesan datos (por ejemplo, [Ibcpsession](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)) analizan filas de datos que se esperan que la longitud de los datos en el archivo de datos sea idéntica a la longitud de los datos especificados en la tabla de base de datos, vista o columna de selección lista. Por ejemplo, los datos de una columna de base de datos definidos como `char(13)` deben estar representados por 13 caracteres por cada fila de datos del archivo. Los datos de longitud fija pueden tener como prefijo un indicador nulo si la columna de base de datos permite valores nulos.  
  
-   Cuando se copian datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el archivo de datos debe tener datos para cada columna de la tabla de base de datos. Cuando se copian datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], los datos de todas las columnas de la tabla de base de datos, la vista o el conjunto de resultados de la instrucción SELECT se copian en el archivo de datos.  
  
-   Cuando se copian datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la posición ordinal de una columna en el archivo de datos debe ser idéntica a la de la columna en la tabla de base de datos. Cuando se copian datos desde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], **BCPExec** método coloca los datos basándose en la posición ordinal de la columna en la tabla de base de datos.  
  
-   Si un tipo de datos de base de datos es de longitud variable (por ejemplo, `varbinary(22)`) o si una columna de base de datos puede contener valores NULL, se antepone a los datos del archivo de datos un indicador de longitud o nulo. El ancho del indicador varía en función del tipo de datos y de la versión de copia masiva. El [ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) opción BCP_OPTION_FILEFMT del método proporciona compatibilidad entre los archivos de datos de copia masiva anteriores y servidores que ejecutan versiones posteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] indicando cuándo el ancho de los indicadores de la datos están inferior a lo esperado.  
  
> [!NOTE]  
>  Para cambiar los valores de formato de datos especificados para un archivo de datos, use la [ibcpsession:: BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) y [ibcpsession:: BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) métodos.  
  
 Las copias masivas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se pueden optimizar para tablas que no contienen índices estableciendo la opción de base de datos **select / bulkcopy**.  
  
## <a name="arguments"></a>Argumentos  
 *pwszTable*[in]  
 Nombre de la tabla de base de datos en o de la que se va a copiar. El nombre puede incluir el nombre de la base de datos o el nombre del propietario. Por ejemplo, "pubs.username.titles", "pubs..titles", "username.titles".  
  
 Si el argumento eDirection está establecido en BCP_DIRECTION_OUT, el argumento pwszTable puede ser el nombre de una vista de base de datos.  
  
 Si el argumento eDirection está establecido en BCP_DIRECTION_OUT y se especifica una instrucción SELECT utilizando la **BCPControl** método antes de la **BCPExec** método se llama, el *pwszTable*argumento debe establecerse en NULL.  
  
 *pwszDataFile*[in]  
 Nombre del archivo de usuario en o del que se va a copiar.  
  
 *pwszErrorFile*[in]  
 Nombre del archivo de error que se va a rellenar con mensajes de progreso, mensajes de error y copias de las filas que, por cualquier razón, no se puedan copiar de un archivo de usuario en una tabla. Si el *pwszErrorFile* argumento se establece en NULL, no se utiliza ningún archivo de error.  
  
 *eDirection*[in]  
 Dirección de la operación de copia, BCP_DIRECTION_IN o BCP_DIRECTION_OUT. BCP_DIRECTION_IN indica una copia de un archivo de usuario en una tabla de base de datos; BCP_DIRECTION_OUT indica una copia de una tabla de base de datos en un archivo de usuario.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor ' para obtener información detallada, use la [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) interfaz.  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
 E_INVALIDARG  
 No se han especificado correctamente uno o varios argumentos. Por ejemplo, se proporcionó un nombre de archivo no válido.  
  
## <a name="see-also"></a>Vea también  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
