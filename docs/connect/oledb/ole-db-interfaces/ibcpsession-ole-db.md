---
title: IBCPSession (OLE DB) | Documentos de Microsoft
description: Interfaz IBCPSession (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 0bd3242d21133f6218a6232b129f7e0109843b33
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El **IBCPSession** interfaz expone la compatibilidad para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] operaciones de copia masiva basadas en archivos. El **IBCPSession** interfaz se expone en el controlador OLE DB para SQL Server en el mismo nivel que Sessions. En el controlador OLE DB para SQL Server, objetos de origen de datos son los generadores de objetos de sesión y las operaciones de copia masiva se especifican en la propiedad de conexión SSPROP_ENABLEBULKCOPY. Además, la propiedad SSPROP_ENABLEFASTLOAD debe establecerse en True.  
  
 Una llamada al método **IDBCreateSession::CreateSession** dará lugar a la creación de un objeto **BulkCopySession** . Todos los métodos de copia masiva basados en archivos que se expongan a través del objeto **IBCPSession** serán entonces invocables con firmas casi similares en la interfaz **IBCPSession** de este objeto **IBCPSession** .  
  
> [!NOTE]  
>  El controlador OLE DB para SQL Server admite las operaciones de copia masiva basadas en memoria a través de la [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) interfaz.  
  
 Para obtener más información sobre cómo usar el controlador OLE DB para SQL Server para operaciones de copia masiva, vea [realizar operaciones de copia masiva](../../oledb/features/performing-bulk-copy-operations.md).  
  
 Para obtener un ejemplo que muestra cómo utilizar el **IBCPSession** de la interfaz, vea [IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Método|Description|  
|------------|-----------------|  
|[Ibcpsession:: BCPColFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|Crea un enlace entre las variables de programa y las columnas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: BCPColumns &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|Establece el número de campos que van a enlazarse a las columnas en una tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: Bcpcontrol &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|Establece las opciones de una operación de copia masiva.|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|Confirma las filas restantes que van a enviarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Ibcpsession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|Realiza la operación de copia masiva.|  
|[Ibcpsession:: BCPInit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|Inicializa la estructura de copia masiva, realiza algunas comprobaciones de errores, comprueba que los datos y los nombres de archivo de formato son correctos y, a continuación, los abre.|  
|[Ibcpsession:: Bcpreadfmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|Lee la información de formato de cada columna en el archivo de formato.|  
|[Ibcpsession:: Bcpwritefmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|Escribe la información de formato de cada columna en el archivo de formato.|  
  
## <a name="see-also"></a>Vea también  
 [Interfaces & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)  
  
  
