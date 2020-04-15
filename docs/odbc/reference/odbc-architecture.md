---
title: Arquitectura ODBC (ODBC Architecture) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07435dc1a5fbe800f2260e914f315cfe93dd8d1b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305136"
---
# <a name="odbc-architecture"></a>Arquitectura ODBC
La arquitectura ODBC tiene cuatro componentes:  
  
-   **Aplicación** Realiza el procesamiento y llama a funciones ODBC para enviar instrucciones SQL y recuperar resultados.  
  
-   **Gerente de conductores** Carga y descarga controladores en nombre de una aplicación. Procesa las llamadas de función ODBC o las pasa a un controlador.  
  
-   **Conductor** Procesa las llamadas a funciones ODBC, envía solicitudes SQL a un origen de datos específico y devuelve resultados a la aplicación. Si es necesario, el controlador modifica la solicitud de una aplicación para que la solicitud se ajuste a la sintaxis admitida por el DBMS asociado.  
  
-   **Fuente de datos** Consiste en los datos a los que el usuario desea acceder y su sistema operativo asociado, DBMS, y la plataforma de red (si existe) utilizado para acceder al DBMS.  
  
 Tenga en cuenta los siguientes puntos sobre la arquitectura ODBC. En primer lugar, pueden existir varios controladores y orígenes de datos, lo que permite a la aplicación acceder simultáneamente a los datos de más de un origen de datos. En segundo lugar, la API ODBC se utiliza en dos lugares: entre la aplicación y el Administrador de controladores, y entre el Administrador de controladores y cada controlador. La interfaz entre el Administrador de controladores y los controladores se conoce a veces como la interfaz del proveedor de *servicios,* o *SPI*. Para ODBC, la interfaz de programación de aplicaciones (API) y la interfaz de proveedor de servicios (SPI) son las mismas; es decir, el Administrador de controladores y cada controlador tienen la misma interfaz para las mismas funciones.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Aplicaciones](../../odbc/reference/applications.md)  
  
-   [El Administrador de controladores](../../odbc/reference/the-driver-manager.md)  
  
-   [Controladores](../../odbc/reference/drivers.md)  
  
-   [Orígenes de datos](../../odbc/reference/data-sources.md)
