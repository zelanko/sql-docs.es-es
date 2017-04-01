---
title: "Utilizar la base de conocimiento predeterminada de DQS | Microsoft Docs"
ms.custom: ""
ms.date: "07/31/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# Utilizar la base de conocimiento predeterminada de DQS
  Este tema describe la base de conocimiento predeterminada **datos de DQS**, que se instala con [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Esta es una base de conocimiento predeterminada pregenerada que contiene los dominios siguientes:  
  
-   **País o región**: contiene el largo convencional (oficial nombre indicado por el país o región) y los nombres cortos (nombre común usado en listas, asignaciones, etc.), abreviatura de dos letras, abreviatura de tres letras y código de tres dígitos para cada ubicación.  El valor principal se establece en el nombre de país largo.  
  
-   **País o región (tres letras iniciales)**: contiene el largo convencional (oficial nombre indicado por el país o región) y los nombres cortos (nombre común usado en listas, asignaciones etc.), abreviatura de dos letras, abreviatura de tres letras y código de tres dígitos para cada ubicación.  Los valores iniciales se establecen en la abreviatura de tres letras del condado.  
  
-   **País o región (dos letras iniciales)**: contiene el largo convencional (oficial nombre indicado por el país o región) y los nombres cortos (nombre común usado en listas, asignaciones, etc.), abreviatura de dos letras, abreviatura de tres letras y código de tres dígitos para cada ubicación.  El valor principal se establece en la abreviatura de dos letras del país.  
  
-   **Estados Unidos - condados**: contiene una lista de los condados de Estados Unidos.  
  
-   **Estados Unidos - apellidos**: contiene una lista de apellidos (apellidos) que se producen 100 o más veces en el censo de 2000.  
  
-   **Coloca US -**: contiene una lista de ubicaciones de los 50 estados, el distrito de Columbia y Puerto Rico extraidos del censo de 2010.  
  
-   **Estados Unidos - estado**: contiene el largo convencional (oficial) nombre y la abreviatura de dos letras para cada estado de Estados Unidos. El valor principal se establece en el nombre convencional de estado.  
  
-   **Estado de Estados Unidos: (encabezado de 2 letras)**: contiene el largo convencional (oficial) nombre y la abreviatura de dos letras para cada estado de Estados Unidos. El valor inicial se establece en la abreviatura de dos letras del nombre de estado.  
  
## Usar la base de conocimiento predeterminada  
 Puede utilizar la base de conocimiento predeterminado DQS, DQS Data, de las maneras siguientes:  
  
-   Inicie y ejecute rápidamente un proyecto de limpieza de calidad de los datos mediante la base de conocimiento predeterminada sin tener primero que crear una base de conocimiento de DQS.  
  
-   Ejecute las actividades Administración de dominio, Detección de conocimiento, Coincidencia de directivas en la base de conocimiento predeterminada. Para ello, haga clic en **Abrir base de conocimiento** en la [Data Quality Client Home Screen](../data-quality-services/data-quality-client-home-screen.md), seleccione la base de conocimiento **Datos de DQS** en la pantalla **Abrir base de conocimiento** y, a continuación, seleccione la actividad necesaria en el área **Seleccione la actividad** . Haga clic en **Siguiente** para continuar.  
  
-   Cree una base de conocimiento con la base de conocimiento predeterminada. Para crear una base de conocimiento a partir de una base de conocimiento existente, vea [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md).  
  
-   Utilizar en la [componente de limpieza DQS en Integration Services](http://go.microsoft.com/fwlink/?LinkId=238830) y [complemento de Master Data Services para Excel](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md).  
  
## Vea también  
 [Bases de conocimiento y dominios de DQS](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  