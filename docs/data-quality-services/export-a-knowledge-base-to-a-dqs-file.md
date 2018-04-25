---
title: Exportar una base de conocimiento a un archivo .dqs | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a324ead5-c8aa-4e26-abe3-ef415add00f8
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9b3656ddd9a9c5016e3e404f5a803f4bdc25d7c8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="export-a-knowledge-base-to-a-dqs-file"></a>Exportar una base de conocimiento a un archivo .dqs

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo exportar una base de conocimiento completa a un archivo de datos .dqs en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Puede exportar un dominio o una base de conocimiento completa a un archivo de datos. Para información sobre cómo exportar un dominio, vea [Exportar un dominio a un archivo .dqs](../data-quality-services/export-a-domain-to-a-dqs-file.md).  
  
 Exportar una base de conocimiento a un archivo .dqs e importarlo después como otra base de conocimiento simplifica el proceso de generación del conocimiento, lo que permite ahorrar tiempo y esfuerzo. Le permite compartir con los demás una base de conocimiento y su conocimiento. El archivo .dqs contendrá toda la información de la base de conocimiento, incluido los dominios y la directiva de coincidencia, salvo la información de datos de referencia adjunta. Debe volver a adjuntar los dominios necesarios a los servicios de datos de referencia adecuados, si es necesario, después de importar el archivo .dqs. Se exportan tanto los datos publicados como los no publicados en una base de conocimiento.  
  
 El archivo de datos .dqs creado por el proceso de exportación se cifra, por lo que no se puede ver el contenido.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para exportar una base de conocimiento a un archivo de datos .dqs, debe haber creado y abierto la base de conocimiento. No es necesario que disponga de un archivo .dqs; se creará uno automáticamente.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para exportar una base de conocimiento a un archivo de datos .dqs.  
  
##  <a name="Export"></a> Export a knowledge base to a .dqs file  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra una base de conocimiento en la actividad Administración de dominios.  
  
3.  En la página Administración de dominios (con cualquier pestaña seleccionada), haga clic en el icono **Exportar datos de la base de conocimiento** situado encima de la lista de dominios y, a continuación, haga clic en **Exportar base de conocimiento**. O bien, haga clic con el botón secundario en la lista **Dominios** , mantenga el mouse sobre **Exportar**y, a continuación, haga clic en **Exportar base de conocimiento**.  
  
4.  En el cuadro de diálogo **Exportar a un archivo de datos**, desplácese a la carpeta en la que quiere guardar el archivo, asígnele un nombre o conserve el nombre de la base de conocimiento, mantenga seleccionada la opción **Archivos de datos DQS (\*.dqs)** en la lista **Guardar como tipo** y, luego, haga clic en **Guardar**.  
  
5.  En el cuadro de diálogo **Exportar base de conocimiento** , compruebe que la línea de estado indica que se ha completado la exportación. Haga clic en **Aceptar**.  
  
##  <a name="FollowUp"></a> Seguimiento: después de exportar un dominio a un archivo .dqs  
 Después de exportar una base de conocimiento a un archivo .dqs, puede importarla en el mismo [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] (con un nuevo nombre) o en otro [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
  
