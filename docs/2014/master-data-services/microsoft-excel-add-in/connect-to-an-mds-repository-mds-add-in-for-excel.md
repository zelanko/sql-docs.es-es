---
title: Conectarse a un repositorio MDS (complemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8f427312-4c09-4c8b-b9f9-8b235557a74b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5f29cdaad3f362c190372ec510f24cb67efe15f7
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961395"
---
# <a name="connect-to-an-mds-repository-mds-add-in-for-excel"></a>Conectarse a un repositorio MDS (complemento MDS para Excel)
  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], debe conectarse a un repositorio MDS para poder cargar o publicar datos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
### <a name="to-connect-to-an-mds-repository"></a>Para conectarse a un repositorio MDS  
  
1.  En MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], en la pestaña **Datos maestros** , en el grupo **Conectar y cargar** , haga clic en la flecha situada debajo del botón **Conectar** y haga clic en **Administrar conexiones**.  
  
2.  En el cuadro de diálogo **Administrar conexiones** , en la sección **Nueva conexión** , haga clic en **Crear una nueva conexión**.  
  
3.  Haga clic en **Nueva**.  
  
4.  En el cuadro de diálogo **Agregar nueva conexión** , en el campo **Descripción** , escriba una descripción de la conexión. Esta conexión se muestra al hacer clic en la flecha situada debajo del botón **Conectar** en la barra de herramientas.  
  
5.  En el cuadro **Dirección del servidor MDS**, escriba la dirección URL de la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]; por ejemplo, http://contoso/mds.  
  
    > [!NOTE]  
    >  Asegúrese de usar el nombre del equipo; no utilice "localhost".  
  
6.  Haga clic en **OK**. El nombre se muestra en la sección **Conexiones existentes** .  
  
7.  Opcionalmente, haga clic en **Probar** para probar la conexión. Se muestra un cuadro de diálogo de confirmación o de error. Haga clic en **Aceptar** para cerrarlo.  
  
8.  Haga clic en **Conectar**. Se muestra el panel **Master Data Services** .  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Cargar datos de MDS en Excel](export-data-to-excel-from-master-data-services.md)  
  
-   [Filtre los datos antes de cargar &#40;Complemento MDS para Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Consulte también  
 [Conexiones &#40;complemento MDS para Excel&#41;](connections-mds-add-in-for-excel.md)  
  
  
