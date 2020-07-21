---
title: Enlace de un informe con un origen de datos compartido | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c5aa5e504c8434d3634b903c08b6a03c0e62345c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081423"
---
# <a name="bind-a-report-to-a-shared-data-source-ssrs"></a>Enlazar un informe con un origen de datos compartido (SSRS)
  En algunos casos (por ejemplo, al mover un informe de un servidor de prueba a uno de producción), es posible que quiera guardar el archivo en el equipo local y, después, cargarlo en otro servidor de informes. Al cargar el informe en el servidor nuevo, debe volver a enlazarlo con un origen de datos compartido almacenado en el servidor de informes nuevo. Si no vuelve a enlazar el informe, no funcionará correctamente cuando se acceda a él desde el servidor de informes nuevo.  
  
> [!IMPORTANT]  
>  Antes de volver a enlazar un informe con un origen de datos compartido, el origen de datos debe existir en el servidor de informes o en la biblioteca de SharePoint. Para más información sobre orígenes de datos, vea [Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
## <a name="to-bind-a-report-to-a-shared-data-source-on-a-report-server-running-in-native-mode"></a>Para enlazar un informe con un origen de datos compartido en un servidor de informes que se ejecuta en modo nativo  
  
1.  En el portal web, haga clic en el botón de puntos suspensivos (...) en la esquina superior derecha del icono de informe > **Administrar**.  

2.  Haga clic en **Orígenes de datos**.  
  
3.  Haga clic en **Un origen de datos compartido** y, después, navegue hasta el origen de datos con el que quiera enlazar el informe.  
  
4.  Seleccione el origen de datos y, después haga clic en **Guardar**.  
  
5.  Haga clic en **Aplicar**.  
  
     Ahora el informe está enlazado con el origen de datos seleccionado.  
  
## <a name="to-bind-a-report-to-a-shared-data-source-on-a-report-server-running-in-sharepoint-integrated-mode"></a>Para enlazar un informe con un origen de datos compartido en un servidor de informes que se ejecuta en el modo integrado de SharePoint  
  
1.  Si la biblioteca aún no está abierta, haga clic en su nombre en la barra Inicio rápido. Si no aparece el nombre de la biblioteca, haga clic en **Ver todo el contenido del sitio**y, a continuación, haga clic en el nombre de la biblioteca.  
  
2.  Seleccione el informe y haga clic en la flecha hacia abajo.  
  
3.  Haga clic en **Administrar orígenes de datos**.  
  
4.  Haga clic en **dataSource1**.  
  
5.  En el área **Tipo de conexión** , compruebe si está seleccionado **Origen de datos compartido** .  
  
6.  En el área **Vínculo a origen de datos**, haga clic en el botón de puntos suspensivos (...).  
  
7.  Busque el origen de datos que desee usar.  
  
8.  Seleccione el origen de datos y haga clic en **Aceptar**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Haga clic en **Cerrar**.  
  
## <a name="see-also"></a>Consulte también  
 [Cargar documentos en una biblioteca de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)   
 [Creación de cadenas de conexión de datos - Generador de informes y SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
  
