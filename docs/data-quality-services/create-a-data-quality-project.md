---
title: Crear un proyecto de calidad de datos | Microsoft Docs
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
f1_keywords:
- sql13.dqs.dqproject.newdqproject.f1
helpviewer_keywords:
- create,data quality project
- data quality project,create
ms.assetid: 19c52d2b-d28e-4449-ab59-5fe0dc326cd9
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 11522ee0ad69880363910f06af8a25904ede7b86
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="create-a-data-quality-project"></a>Crear un proyecto de calidad de datos

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo crear un proyecto de calidad de datos mediante [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Un proyecto de calidad de datos se utiliza para ejecutar la actividad de limpieza o de búsqueda de coincidencias en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Debe disponer de una base de conocimiento apropiada para su uso en el proyecto de calidad de datos para la actividad de limpieza o de búsqueda de coincidencias.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe disponer del rol dqs_kb_editor o dqs_kb_operator en la base de datos DQS_MAIN para crear un proyecto de calidad de datos.  
  
##  <a name="Create"></a> Crear un proyecto de calidad de datos  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Nuevo proyecto de calidad de datos**.  
  
3.  En la pantalla **Nuevo proyecto de calidad de datos** :  
  
    1.  En el cuadro **Nombre** , escriba el nombre del nuevo proyecto de calidad de datos.  
  
    2.  (Opcional) En el cuadro **Descripción** , escriba una descripción para el nuevo proyecto de calidad de datos.  
  
    3.  Haga clic en la lista **Usar base de conocimiento** para seleccionar la base de conocimiento que se utilizará para el proyecto de calidad de datos. El área **Detalles de la base de conocimiento: <nombre_base_conocimiento>** situada en el lado derecho muestra los nombres de dominio disponibles en la base de conocimiento seleccionada.  
  
    4.  En el área **Seleccione la actividad** , haga clic en la actividad que desea realizar utilizando este proyecto de calidad de datos:  
  
        -   **Limpieza**: seleccione esta actividad para limpiar los datos de origen.  
  
        -   **Coincidencia**: seleccione esta actividad para realizar la búsqueda de coincidencias. Esta actividad solo está disponible si la base de conocimiento seleccionada para el proyecto de calidad de datos contiene una directiva de coincidencia.  
  
4.  Haga clic en **Crear** para crear un proyecto de calidad de datos.  
  
##  <a name="FollowUp"></a> Seguimiento: después de crear un proyecto de calidad de datos  
 Una vez creado el proyecto de calidad de datos, aparecerá un asistente que podrá utilizar para realizar la actividad seleccionada: limpieza o búsqueda de coincidencias. Para más información sobre las actividades de limpieza y de búsqueda de coincidencias, vea [Limpieza de datos](../data-quality-services/data-cleansing.md) y [Coincidencia de datos](../data-quality-services/data-matching.md).  
  
  
