---
title: Usar la base de conocimiento predeterminada de DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 40a69447a0aff678cfd53a75603200b467a542c7
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56016316"
---
# <a name="using-the-dqs-default-knowledge-base"></a>Utilizar la base de conocimiento predeterminada de DQS
  En este tema se describe la base de conocimiento predeterminada, **Datos de DQS**, que se instala con [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Esta es una base de conocimiento predeterminada pregenerada que contiene los dominios siguientes:  
  
-   **País o región**: Contiene el largo convencional (nombre válido según se designe por el país o región) y los nombres cortos (nombre común usado en las listas, en el mapa, etc.), abreviatura de dos letras, abreviatura de tres letras y código de tres dígitos para cada ubicación.  El valor principal se establece en el nombre de país largo.  
  
-   **País o región (tres letras iniciales)**: Contiene el largo convencional (nombre válido según se designe por el país o región) y los nombres cortos (nombre común usado en las listas, en el mapa etc.), abreviatura de dos letras, abreviatura de tres letras y código de tres dígitos para cada ubicación.  Los valores iniciales se establecen en la abreviatura de tres letras del condado.  
  
-   **País o región (dos letras iniciales)**: Contiene el largo convencional (nombre válido según se designe por el país o región) y los nombres cortos (nombre común usado en las listas, en el mapa, etc.), abreviatura de dos letras, abreviatura de tres letras y código de tres dígitos para cada ubicación.  El valor principal se establece en la abreviatura de dos letras del país.  
  
-   **EE. UU. - los condados**: Contiene una lista de los condados de Estados Unidos.  
  
-   **EE. UU. - apellido**: Contiene una lista de apellidos (apellidos) que se producen 100 o más veces en el censo de 2000.  
  
-   **EE. UU. - coloca**: Contiene una lista de sitios para los 50 estados, el distrito de Columbia y Puerto Rico extraidos del censo de 2010.  
  
-   **EE. UU. - estado**: Contiene el largo convencional (oficial) nombre y la abreviatura de dos letras para cada estado de Estados Unidos. El valor principal se establece en el nombre convencional de estado.  
  
-   **US - Estados (encabezado de 2 letras)**: Contiene el largo convencional (oficial) nombre y la abreviatura de dos letras para cada estado de Estados Unidos. El valor inicial se establece en la abreviatura de dos letras del nombre de estado.  
  
## <a name="using-the-default-knowledge-base"></a>Usar la base de conocimiento predeterminada  
 Puede utilizar la base de conocimiento predeterminado DQS, DQS Data, de las maneras siguientes:  
  
-   Inicie y ejecute rápidamente un proyecto de limpieza de calidad de los datos mediante la base de conocimiento predeterminada sin tener primero que crear una base de conocimiento de DQS.  
  
-   Ejecute las actividades Administración de dominio, Detección de conocimiento, Coincidencia de directivas en la base de conocimiento predeterminada. Para ello, haga clic en **Abrir base de conocimiento** en la [Data Quality Client Home Screen](../../2014/data-quality-services/data-quality-client-home-screen.md), seleccione la base de conocimiento **Datos de DQS** en la pantalla **Abrir base de conocimiento** y, a continuación, seleccione la actividad necesaria en el área **Seleccione la actividad** . Haga clic en **Siguiente** para continuar.  
  
-   Cree una base de conocimiento con la base de conocimiento predeterminada. Para crear una base de conocimiento a partir de una base de conocimiento existente, vea [Create a Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md).  
  
-   Úsela en el [componente Limpieza de DQS de Integration Services](https://go.microsoft.com/fwlink/?LinkId=238830) y [Complemento Master Data Services para Excel](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md).  
  
## <a name="see-also"></a>Vea también  
 [Bases de conocimiento y dominios de DQS](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
