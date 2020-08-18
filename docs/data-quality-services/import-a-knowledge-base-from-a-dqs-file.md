---
description: Importar una base de conocimiento desde un archivo .dqs
title: Importar una base de conocimiento desde un archivo .dqs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
author: swinarko
ms.author: sawinark
ms.openlocfilehash: c6be16bf484f3b5f6f55afaaacbeda8d2bb6d341
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491575"
---
# <a name="import-a-knowledge-base-from-a-dqs-file"></a>Importar una base de conocimiento desde un archivo .dqs

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  En este tema se describe cómo importar una base de conocimiento completa desde un archivo de datos .dqs en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Para crear el archivo de datos, debe exportar una base de conocimiento existente desde la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] (vea [exportar una Base de conocimiento a un archivo .dqs](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)).  
  
 El uso de un archivo de datos .dqs para exportar el contenido de una base de conocimiento e importarlo a continuación en otra base de conocimiento del mismo [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] o de otro [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] simplifica el proceso de generación del conocimiento, lo que permite ahorrar tiempo y esfuerzo. Le permite compartir con los demás una base de conocimiento y su conocimiento, lo que se traduce en un ahorro de tiempo. El archivo .dqs contendrá toda la información de la base de conocimiento, incluido los dominios y la directiva de coincidencia, salvo la información de datos de referencia adjunta. Se importarán tanto los datos publicados como los no publicados.  
  
 El archivo de datos .dqs está cifrado, por lo que no se puede ver.  
  
 Al importar una base de conocimiento, puede utilizar el mismo nombre, a menos que este exista ya en la aplicación cliente, en cuyo caso deberá cambiarlo.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
 Para importar una base de conocimiento desde un archivo de .dqs, antes debe haberla exportado al archivo .dqs.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para importar una base de conocimiento desde un archivo de datos .dqs.  
  
##  <a name="import-a-knowledge-base-from-a-dqs-file"></a><a name="Import"></a> Importar una base de conocimiento desde un archivo. DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Nueva base de conocimiento**.  
  
3.  Escriba un nombre para la base de conocimiento.  
  
4.  Haga clic en la flecha abajo de **Crear base de conocimiento a partir de**y, a continuación, seleccione **Importar desde el archivo DQS**.  
  
5.  En **Seleccionar archivo de datos**, haga clic en **Examinar**.  
  
6.  En el cuadro de diálogo **Importar de archivo de datos** , desplácese a la carpeta que contiene el archivo .dqs que desea importar y, a continuación, haga clic en el nombre del archivo. Haga clic en **Abrir**.  
  
7.  Compruebe que en la lista **Dominios** aparecen la base de conocimiento y los dominios correctos.  
  
8.  Seleccione la actividad que desea realizar y, a continuación, haga clic en **Crear**.  
  
9. En el cuadro de diálogo **Importar base de conocimiento** , compruebe que la línea de estado indica que se ha completado la importación. Haga clic en **OK**.  
  
10. Finalice las tareas de detección de conocimiento, administración de dominios o directiva de coincidencia que necesita realizar y, a continuación, haga clic en **Finalizar**.  
  
11. Haga clic en **Publicar** para publicar el conocimiento en la base de conocimiento, o en **No** si prefiere no hacerlo.  
  
12. Si opta por publicar la base de conocimiento, haga clic en **Aceptar**.  
  
13. En la página de inicio de Data Quality Services, compruebe que la base de conocimiento aparece debajo de **Base de conocimiento reciente**.  
  
##  <a name="follow-up-after-importing-a-knowledge-base-from-a-dqs-file"></a><a name="FollowUp"></a> Seguimiento: después de importar una base de conocimiento desde un archivo .dqs  
 Después de importar una base de conocimiento desde un archivo .dqs, puede agregar conocimiento a la base de conocimiento o utilizarla en un proyecto de limpieza o de búsqueda de coincidencias, dependiendo de su contenido. Para más información, vea [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../data-quality-services/managing-a-domain.md), [Administrar un dominio compuesto](../data-quality-services/managing-a-composite-domain.md), [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md), [Limpieza de datos](../data-quality-services/data-cleansing.md) o [Coincidencia de datos](../data-quality-services/data-matching.md).  
  
  
