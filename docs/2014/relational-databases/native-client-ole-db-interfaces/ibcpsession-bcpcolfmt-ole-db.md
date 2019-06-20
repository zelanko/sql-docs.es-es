---
title: IBCPSession::BCPColFmt (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPColFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPColFmt method
ms.assetid: 2852f4ba-f1c6-4c4c-86b2-b77e4abe70de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e896f3e04d24becf136b7abefcff9dbe97fa0970
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240269"
---
# <a name="ibcpsessionbcpcolfmt-ole-db"></a>IBCPSession::BCPColFmt (OLE DB)
  Crea un enlace entre las variables de programa y las columnas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPColFmt(   
DBORDINALidxUserDataCol,  
inteUserDataType,  
intcbIndicator,  
intcbUserData,  
BYTE *pbUserDataTerm,  
intcbUserDataTerm,  
DBORDINALidxServerCol);  
```  
  
## <a name="remarks"></a>Comentarios  
 El método **BCPColFmt** se usa para crear un enlace entre los campos de archivo de datos BCP y las columnas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Toma como parámetros la longitud, el tipo, el terminador y la longitud de prefijo de una columna y establece cada una de estas propiedades para campos individuales.  
  
 Si el usuario elige el modo interactivo, se llama a este método dos veces; una para establecer el formato de columna en función de los valores predeterminados (según el tipo de columna de servidor) y otra para establecer el formato en función del tipo de columna elegido por el cliente durante el modo interactivo para cada columna.  
  
 En modos no interactivos, se llama a este método una sola vez por columna para establecer el tipo de cada columna en el tipo de caracteres o tipo nativo y para establecer los terminadores de columna y fila.  
  
 El método **BCPColFmt** permite especificar el formato de archivo de usuario para las copias masivas. Para la copia masiva, un formato contiene los componentes siguientes:  
  
-   Una asignación de los campos de archivo de usuario a las columnas de base de datos.  
  
-   El tipo de datos de cada campo de archivo de usuario.  
  
-   La longitud del indicador opcional para cada campo.  
  
-   La longitud máxima de los datos por campo de archivo de usuario.  
  
-   La secuencia de bytes de terminación opcional para cada campo.  
  
-   La longitud de la secuencia de bytes de terminación opcional.  
  
 En cada llamada a **BCPColFmt** se especifica el formato para un campo de archivo de usuario. Por ejemplo, para cambiar la configuración predeterminada de tres campos en un archivo de datos de usuario de cinco campos, primero debe llamar a `BCPColumns(5)`y, a continuación, debe llamar a **BCPColFmt** cinco veces, con tres de cuyas llamadas establecerá el formato personalizado. Para las dos llamadas restantes, establezca *eUserDataType* en BCP_TYPE_DEFAULT y establezca *cbIndicator*, *cbUserData*y *cbUserDataTerm* en 0, BCP_VARIABLE_LENGTH y 0, respectivamente. Este procedimiento copia las cinco columnas, tres con el formato personalizado y dos con el formato predeterminado.  
  
> [!NOTE]  
>  Debe llamar al método [IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md) antes de realizar cualquier llamada a **BCPColFmt**. Debe llamar a **BCPColFmt** una vez para cada columna del archivo de usuario. Si llama más de una vez a **BCPColFmt** para cualquier columna de archivo de usuario, se generará un error.  
  
 No es necesario copiar todos los datos de un archivo de usuario en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para omitir una columna, debe especificar el formato de los datos de la columna estableciendo el parámetro idxServerCol en 0. Si desea omitir un campo, necesitará toda la información para que el método funcione correctamente.  
  
 **Nota** La función [IBCPSession::BCPWriteFmt](ibcpsession-bcpwritefmt-ole-db.md) puede usarse para conservar la especificación de formato que se proporciona a través de **BCPColFmt**.  
  
## <a name="arguments"></a>Argumentos  
 *idxUserDataCol*[in]  
 Índice de campo del archivo de datos del usuario.  
  
 *eUserDataType*[in]  
 Tipo de datos de campo del archivo de datos del usuario. Los tipos de datos disponibles se muestran en el archivo de encabezado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (sqlncli.h) con el formato BCP_TYPE_XXX como, por ejemplo, BCP_TYPE_SQLINT4. Si se especifica el valor BCP_TYPE_DEFAULT, el proveedor intenta usar el mismo tipo que el tipo de columna de tabla o vista. Operaciones de copia masiva fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en un archivo cuando el `eUserDataType` argumento sea BCP_TYPE_SQLDECIMAL o BCP_TYPE_SQLNUMERIC:  
  
-   Si la columna de origen no es decimal o numérica, se usarán la precisión y la escala predeterminadas.  
  
-   Si la columna de origen es decimal o numérica, se usarán la precisión y la escala de la columna de origen.  
  
 *cbIndicator*[in]  
 Longitud de prefijo del campo. El valor predeterminado es BCP_PREFIX_DEFAULT. Las longitudes válidas para el prefijo son 0, 1, 2, 4 y 8. Un prefijo de tamaño 8 se usa normalmente para indicar que el campo está fragmentado. Se usa para realizar copias masivas de columnas de tipo de valor grande de forma eficaz.  
  
 *cbUserData*[in]  
 Longitud máxima (en bytes) de los datos de este campo del archivo de usuario, sin incluir la longitud de los indicadores de longitud o terminadores.  
  
 Establecer `cbUserData` en BCP_LENGTH_NULL se indica que todos los valores de los datos de campos del archivo están, o debería estar establecido en NULL. Establecer `cbUserData` en BCP_LENGTH_VARIABLE se indica que el sistema debe determinar la longitud de datos para cada campo. Para algunos campos, esto podría significar que se genera un indicador de longitud o NULL que precede a los datos en una copia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o que se espera el indicador en los datos copiados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caracteres y tipos de datos binarios, `cbUserData` puede ser BCP_LENGTH_VARIABLE, BCP_LENGTH_NULL, 0 o algún valor positivo. Si `cbUserData` es BCP_LENGTH_VARIABLE, el sistema utiliza un indicador de longitud, si está presente, o una secuencia de terminador para determinar la longitud de los datos. Si se proporciona un indicador de longitud y una secuencia de terminador, la copia masiva usa aquél por el que se copia la mínima cantidad de datos. Si `cbUserData` es BCP_LENGTH_VARIABLE, los datos de tipo es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caracteres o tipo binaria, y si se especifica ni un indicador de longitud ni una secuencia de terminador, el sistema devuelve un mensaje de error.  
  
 Si `cbUserData` es 0 o un valor positivo, el sistema utiliza `cbUserData` como la longitud máxima de los datos. Sin embargo, si además un positivo `cbUserData`, se proporciona una secuencia de longitud de indicador o un terminador, el sistema determina la longitud de datos mediante el método que da como resultado la menor cantidad de datos que se va a copiar.  
  
 El `cbUserData` valor representa el número de bytes de datos. Si los datos de caracteres se representan mediante caracteres anchos de Unicode, un positivo `cbUserData` el valor del parámetro representa el número de caracteres multiplicado por el tamaño, en bytes, de cada carácter.  
  
 *pbUserDataTerm*[size_is][in]  
 Secuencia de terminador que se va a usar para el campo. Este parámetro es principalmente útil para los tipos de datos de caracteres porque todos los demás tipos son de longitud fija o, en el caso de los datos binarios, requieren un indicador de longitud que grabe con precisión el número de bytes presentes.  
  
 Para evitar la terminación de los datos extraídos o indicar que no se terminen los datos de un archivo de usuario, establezca este parámetro en NULL.  
  
 Si se usa más de un medio para especificar una longitud de columna de usuario (como un terminador y un indicador de longitud, o un terminador y una longitud máxima de columna), la copia masiva elige aquél por el que se copia la cantidad mínima de datos.  
  
 La API de copia masiva realiza la conversión de caracteres Unicode a MBCS según sea necesario. Se deben extremar las precauciones para asegurarse de que se establece correctamente la cadena de bytes del terminador y la longitud de la cadena de bytes.  
  
 *cbUserDataTerm*[in]  
 Longitud (en bytes) de la secuencia de terminador que va a usarse para la columna. Si no hay ningún terminador presente o no se desea uno en los datos, establezca este valor en 0.  
  
 *idxServerCol*[in]  
 Posición ordinal de la columna en la tabla de base de datos. El primer número de columna es 1. La posición ordinal de una columna la notifica el método **IColumnsInfo::GetColumnInfo** u otros métodos similares. Si este valor es 0, la copia masiva omite el campo en el archivo de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor; para obtener información detallada, use la interfaz [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) .  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, no se llamó al método [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) antes de llamar a este método.  
  
 E_INVALIDARG  
 El argumento no era válido.  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
## <a name="see-also"></a>Vea también  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../native-client/features/performing-bulk-copy-operations.md)  
  
  
