---
description: Instalar el Software (ODBC)
title: Instalación del software (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], installing
- installing ODBC driver for Oracle [ODBC]
ms.assetid: dfac8ade-eebe-4ebe-a199-feb740ed5bae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe161ef45ef91f67317d7a0b465e00d3d2045c40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449477"
---
# <a name="installing-the-software-odbc"></a>Instalar el Software (ODBC)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC para Oracle es uno de los componentes de acceso a datos. Acompaña a otros componentes ODBC, como el administrador de orígenes de datos ODBC, y ya deben estar instalados. El controlador también puede encontrarse en "controladores y otras descargas" en el sitio web en línea de los servicios de soporte técnico de Microsoft, en [www.Microsoft.com](https://www.microsoft.com).  
  
 El software de red debe instalarse según su propia documentación. El controlador ODBC para Oracle no requiere ninguna consideración de instalación especial, siempre que se admita el software de red.  
  
 El software de Oracle debe instalarse según su propia documentación. El controlador ODBC para Oracle normalmente no requiere ninguna consideración de instalación especial, siempre que el controlador admita la versión. Sin embargo, para mantener los productos compatibles, instale el controlador ODBC para Oracle en último lugar para asegurarse de que tiene la versión más reciente del controlador. Oracle mantiene un sitio FTP público donde envía, entre otras cosas, revisiones a los productos de servidor de Oracle y al componente de cliente que se suministra con los productos de servidor. Estas revisiones son necesarias para el correcto funcionamiento de varios productos y tecnologías de Microsoft. Para obtener más información acerca de este sitio, consulte [revisiones de software de Oracle](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!CAUTION]  
>  La instalación del software de Oracle a través de la DAC de Windows y MDAC puede sobrescribir las versiones actuales de MDAC. Si surgen problemas con los componentes ODBC, vuelva a instalar MDAC.
