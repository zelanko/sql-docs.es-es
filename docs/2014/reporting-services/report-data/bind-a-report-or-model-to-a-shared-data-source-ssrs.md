---
title: Enlazar un informe o un modelo con un origen de datos compartido (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ca6d2e98bc631a675aee3d4968103c9981775019
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52521770"
---
# <a name="bind-a-report-or-model-to-a-shared-data-source-ssrs"></a>Enlazar un informe o un modelo con un origen de datos compartido (SSRS)
  En algunos casos (por ejemplo, al mover un informe o un modelo de un servidor de prueba a un servidor de producción), puede que desee guardar el archivo en el equipo local y, a continuación, cargarlo en otro servidor de informes. Al cargar el informe o el modelo en el servidor nuevo, debe volver a enlazarlo con un origen de datos compartido almacenado en el servidor de informes nuevo. Si no vuelve a enlazar el informe o el modelo, no funcionará correctamente cuando se obtenga acceso a él desde el servidor de informes nuevo.  
  
> [!IMPORTANT]  
>  Para poder volver a enlazar un informe o un modelo con un origen de datos compartido, el origen de datos debe existir en el servidor de informes o en la biblioteca de SharePoint. Para más información sobre orígenes de datos, vea [Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md).  
  
### <a name="to-bind-a-report-or-model-to-a-shared-data-source-on-a-report-server-running-in-native-mode"></a>Para enlazar un informe o un modelo con un origen de datos compartido en un servidor de informes que se ejecuta en modo nativo  
  
1.  En el **Administrador de informes**, haga clic en el nombre del informe o el modelo cargado en el servidor.  
  
     Se abre la pestaña Propiedades.  
  
2.  Haga clic en **Orígenes de datos**.  
  
3.  Haga clic en **Examinar**y, a continuación, navegue hasta el origen de datos con el que desea enlazar el informe o el modelo.  
  
4.  Seleccione el origen de datos y, a continuación, haga clic en **Aceptar**.  
  
5.  Haga clic en **Aplicar**.  
  
     El informe o el modelo ya está enlazado con el origen de datos seleccionado.  
  
### <a name="to-bind-a-report-or-model-to-a-shared-data-source-on-a-report-server-running-in-sharepoint-integrated-mode"></a>Para enlazar un informe o un modelo con un origen de datos compartido en un servidor de informes que se ejecuta en el modo integrado de SharePoint  
  
1.  Si la biblioteca aún no está abierta, haga clic en su nombre en la barra Inicio rápido. Si no aparece el nombre de la biblioteca, haga clic en **Ver todo el contenido del sitio**y, a continuación, haga clic en el nombre de la biblioteca.  
  
2.  Seleccione el informe o el modelo y haga clic en la flecha hacia abajo.  
  
3.  Haga clic en **Administrar orígenes de datos**.  
  
4.  Haga clic en **dataSource1**.  
  
5.  En el área **Tipo de conexión** , compruebe si está seleccionado **Origen de datos compartido** .  
  
6.  En el área **Vínculo a origen de datos**, haga clic en el botón de puntos suspensivos (...).  
  
7.  Busque el origen de datos que desee usar.  
  
8.  Seleccione el origen de datos y haga clic en **Aceptar**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Haga clic en **Cerrar**.  
  
## <a name="see-also"></a>Vea también  
 [Cargar un archivo o un informe &#40;Administrador de informes&#41;](../reports/upload-a-file-or-report-report-manager.md)   
 [Cargar documentos en una biblioteca de SharePoint &#40;Reporting Services en modo de SharePoint&#41;](../upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)   
 [Crear, eliminar o modificar un origen de datos compartido &#40;Administrador de informes&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
