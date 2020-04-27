---
title: Modificar procedimientos almacenados que utilizan propiedades de búsqueda de texto completo no incluidas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5204b27fb4745f8005a328dc62503f7db418387d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093849"
---
# <a name="modify-stored-procedures-that-use-discontinued-full-text-search-properties"></a>Modificar los procedimientos almacenados que utilizan propiedades de búsqueda de texto completo no incluidas
  Para asegurarse de que sus procedimientos almacenados funcionen correctamente, debería modificar los procedimientos existentes y quitar aquellas propiedades y configuraciones relacionadas con la búsqueda de texto completo que se han quitado o han quedado desusadas.  
  
## <a name="component"></a>Componente  
 Búsqueda de texto completo  
  
## <a name="description"></a>Descripción  
 Los siguientes parámetros y propiedades relacionados con la búsqueda de texto completo se han quitado.  
  
-   **DataTimeout**  
  
-   **ConnectTimeout**  
  
-   **Clean_up**  
  
-   **LogSize**  
  
 Los siguientes parámetros y propiedades relacionados con la búsqueda de texto completo se han quitado o han quedado desusados:  
  
-   'Path' del catálogo de texto completo. El Catálogo de texto completo será un objeto lógico sin una ruta de acceso al archivo en el sistema.  
  
-   La función de habilitar o deshabilitar en SP_FULLTEXT_DATABASE ya no tiene ningún efecto cuando las bases de datos están habilitadas para las búsquedas de texto completo en todo momento y de forma predeterminada en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique sus procedimientos almacenados para quitar estas propiedades.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
