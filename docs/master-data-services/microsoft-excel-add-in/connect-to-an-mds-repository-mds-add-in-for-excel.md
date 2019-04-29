---
title: Conectarse a un repositorio MDS (complemento MDS para Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8f427312-4c09-4c8b-b9f9-8b235557a74b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: b287bb547b3f151ba26d0f0707f57bf04c8ec163
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62999817"
---
# <a name="connect-to-an-mds-repository-mds-add-in-for-excel"></a>Conectarse a un repositorio MDS (complemento MDS para Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], debe conectarse a un repositorio MDS para poder cargar o publicar datos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
### <a name="to-connect-to-an-mds-repository"></a>Para conectarse a un repositorio MDS  
  
1.  En MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], en la pestaña **Datos maestros** , en el grupo **Conectar y cargar** , haga clic en la flecha situada debajo del botón **Conectar** y haga clic en **Administrar conexiones**.  
  
2.  En el cuadro de diálogo **Administrar conexiones** , en la sección **Nueva conexión** , haga clic en **Crear una nueva conexión**.  
  
3.  Haga clic en **Nueva**.  
  
4.  En el cuadro de diálogo **Agregar nueva conexión** , en el campo **Descripción** , escriba una descripción de la conexión. Esta conexión se muestra al hacer clic en la flecha situada debajo del botón **Conectar** en la barra de herramientas.  
  
5.  En el cuadro **Dirección del servidor MDS**, escriba la dirección URL de la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]; por ejemplo, `https://contoso/mds`.  
  
    > [!NOTE]  
    >  Asegúrese de usar el nombre del equipo; no utilice "localhost".  
  
6.  Haga clic en **Aceptar**. El nombre se muestra en la sección **Conexiones existentes** .  
  
7.  Opcionalmente, haga clic en **Probar** para probar la conexión. Se muestra un cuadro de diálogo de confirmación o de error. Haga clic en **Aceptar** para cerrarlo.  
  
8.  Haga clic en **Conectar**. Se muestra el panel **Master Data Services** .  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)  
  
-   [Filtrar los datos antes de exportar &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Vea también  
 [Conexiones &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
  
