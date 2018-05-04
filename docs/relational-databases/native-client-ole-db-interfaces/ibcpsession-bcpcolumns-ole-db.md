---
title: 'Ibcpsession:: BCPColumns (OLE DB) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPColumns (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColumns method
ms.assetid: c338abe8-9e30-4853-a7c6-b1a6c00095e1
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a4e88b77e8afa2e83df3abada1f063dc18c98663
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Establece el número de campos que van a enlazarse a las columnas en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT BCPColumns(   
      DBCOUNTITEM nColumns);  
```  
  
## <a name="remarks"></a>Comentarios  
 Llama internamente [ibcpsession:: BCPColFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) para establecer los valores predeterminados para los datos de campo. Estos valores predeterminados se obtienen de la información de columna de SQL Server que el proveedor recupera internamente cuando se especifica el nombre de tabla a través de [ibcpsession:: BCPInit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md).  
  
> [!NOTE]  
>  Se puede llamar a este método solamente después de que se haya llamado a **a BCPInit** con un nombre de archivo válido.  
  
 Solo debe llamar a este método si piensa utilizar un formato de archivo de usuario que difiere del valor predeterminado. Para obtener más información sobre una descripción del formato predeterminado del archivo de usuario, vea el método **BCPInit** .  
  
 Después de llamar al método **BCPColumns** , debe llamar al método **BCPColFmt** para cada columna en el archivo de usuario para definir completamente un formato de archivo personalizado.  
  
## <a name="arguments"></a>Argumentos  
 *nColumns*[in]  
 El número total de campos en el archivo de usuario. Aun cuando está preparando para realizar copias masiva de datos del archivo de usuario a una tabla SQL Server y no piensa copiar todos los campos en el archivo de usuario, todavía debe establecer el argumento *nColumns* en el número total de campos de archivo de usuario. Los campos omitidos se pueden especificar a continuación a través de **BCPColFmt**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_FAIL  
 Se produjo un error específico del proveedor; Para obtener información detallada, use la [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) interfaz.  
  
 E_UNEXPECTED  
 No se esperaba la llamada al método. Por ejemplo, no se llamó al método **BCPInit** antes de llamar a este método. También se produce cuando se llama a este método más de una vez para una operación de copia masiva.  
  
 E_OUTOFMEMORY  
 Error de memoria insuficiente.  
  
## <a name="see-also"></a>Vea también  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [Realizar operaciones de copia masiva](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
