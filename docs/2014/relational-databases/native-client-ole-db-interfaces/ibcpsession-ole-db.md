---
title: IBCPSession (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IBCPSession interface
ms.assetid: 00d0311f-8b71-4ad6-824d-0e89119347a3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 142f6ac339e437877c485588333fabb04e0bd66b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212325"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
  La interfaz **IBCPSession** expone compatibilidad con las operaciones de copia masiva basadas en archivos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El **IBCPSession** interfaz se expone en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB en el mismo nivel que Sessions. En el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB, objetos de origen de datos son los generadores de los objetos Session y operaciones de copia masiva se especifican en la propiedad de conexión SSPROP_ENABLEBULKCOPY. Además, la propiedad SSPROP_ENABLEFASTLOAD debe establecerse en True.  
  
 Una llamada al método **IDBCreateSession::CreateSession** dará lugar a la creación de un objeto **BulkCopySession** . Todos los métodos de copia masiva basados en archivos que se expongan a través del objeto **IBCPSession** serán entonces invocables con firmas casi similares en la interfaz **IBCPSession** de este objeto **IBCPSession** .  
  
> [!NOTE]  
>  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite las operaciones de copia masiva basadas en memoria a través de la [IRowsetFastLoad](irowsetfastload-ole-db.md) interfaz.  
  
 Para obtener más información sobre el uso de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB para operaciones de copia masiva, vea [realizar operaciones de copia masiva](../native-client/features/performing-bulk-copy-operations.md).  
  
 Para obtener un ejemplo que muestra cómo usar el **IBCPSession** interfaz, vea [IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Método|Descripción|  
|------------|-----------------|  
|[Ibcpsession:: BCPColFmt &#40;OLE DB&#41;](ibcpsession-bcpcolfmt-ole-db.md)|Crea un enlace entre las variables de programa y las columnas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: BCPColumns &#40;OLE DB&#41;](ibcpsession-bcpcolumns-ole-db.md)|Establece el número de campos que van a enlazarse a las columnas en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: Bcpcontrol &#40;OLE DB&#41;](ibcpsession-bcpcontrol-ole-db.md)|Establece las opciones de una operación de copia masiva.|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md)|Confirma las filas restantes que van a enviarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Ibcpsession &#40;OLE DB&#41;](ibcpsession-bcpexec-ole-db.md)|Realiza la operación de copia masiva.|  
|[Ibcpsession:: BCPInit &#40;OLE DB&#41;](ibcpsession-bcpinit-ole-db.md)|Inicializa la estructura de copia masiva, realiza algunas comprobaciones de errores, comprueba que los datos y los nombres de archivo de formato son correctos y, a continuación, los abre.|  
|[Ibcpsession:: Bcpreadfmt &#40;OLE DB&#41;](ibcpsession-bcpreadfmt-ole-db.md)|Lee la información de formato de cada columna en el archivo de formato.|  
|[Ibcpsession:: Bcpwritefmt &#40;OLE DB&#41;](ibcpsession-bcpwritefmt-ole-db.md)|Escribe la información de formato de cada columna en el archivo de formato.|  
  
## <a name="see-also"></a>Vea también  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
