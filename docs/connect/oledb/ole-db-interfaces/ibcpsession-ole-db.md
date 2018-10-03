---
title: IBCPSession (OLE DB) | Microsoft Docs
description: Interfaz IBCPSession (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 96603d7dcb6215513d67d4db5d29f8a762d57ea8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764933"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La interfaz **IBCPSession** expone compatibilidad con las operaciones de copia masiva basadas en archivos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El **IBCPSession** interfaz se expone en el controlador OLE DB para SQL Server en el mismo nivel que Sessions. En el controlador OLE DB para SQL Server, los objetos de origen de datos son los generadores de los objetos de sesión y las operaciones de copia masiva se especifican en la propiedad de conexión SSPROP_ENABLEBULKCOPY. Además, la propiedad SSPROP_ENABLEFASTLOAD debe establecerse en True.  
  
 Una llamada al método **IDBCreateSession::CreateSession** dará lugar a la creación de un objeto **BulkCopySession** . Todos los métodos de copia masiva basados en archivos que se expongan a través del objeto **IBCPSession** serán entonces invocables con firmas casi similares en la interfaz **IBCPSession** de este objeto **IBCPSession** .  
  
> [!NOTE]  
>  El controlador OLE DB para SQL Server es compatible con las operaciones de copia masiva basadas en memoria a través de la interfaz [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md).  
  
 Para obtener más información sobre cómo usar el controlador OLE DB para SQL Server para operaciones de copia masiva, vea [realizar operaciones de copia masiva](../../oledb/features/performing-bulk-copy-operations.md).  
  
 Para obtener un ejemplo que muestra cómo usar el **IBCPSession** interfaz, vea [IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Método|Descripción|  
|------------|-----------------|  
|[Ibcpsession:: BCPColFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|Crea un enlace entre las variables de programa y las columnas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: BCPColumns &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|Establece el número de campos que van a enlazarse a las columnas en una tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: Bcpcontrol &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|Establece las opciones de una operación de copia masiva.|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|Confirma las filas restantes que van a enviarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Ibcpsession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|Realiza la operación de copia masiva.|  
|[Ibcpsession:: BCPInit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|Inicializa la estructura de copia masiva, realiza algunas comprobaciones de errores, comprueba que los datos y los nombres de archivo de formato son correctos y, a continuación, los abre.|  
|[Ibcpsession:: Bcpreadfmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|Lee la información de formato de cada columna en el archivo de formato.|  
|[Ibcpsession:: Bcpwritefmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|Escribe la información de formato de cada columna en el archivo de formato.|  
  
## <a name="see-also"></a>Ver también  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)  
  
  
