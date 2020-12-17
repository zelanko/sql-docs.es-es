---
title: Propiedades de Alias (pestaña Alias)
description: Use la pestaña Alias del cuadro de diálogo Propiedades para configurar un alias de modo que pueda usar un nombre alternativo al conectarse a una instancia de SQL Server.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 2d1498e2-129c-4ce7-88e5-408e4037243c
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 65558dcdc06b42f3f475fae1b0041909bdff8967
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481716"
---
# <a name="ltaliasgt-properties-alias-tab"></a>Propiedades de &lt;Alias&gt; (pestaña Alias)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

Un alias es un nombre alternativo que se puede utilizar para establecer una conexión. El alias encapsula los elementos necesarios de una cadena de conexión y los expone con un nombre elegido por el usuario. Use la página **Alias** del cuadro de diálogo **Propiedades de \<**Alias name**>** para ver o especificar los elementos de la cadena de conexión de un alias.

## <a name="options"></a>Opciones

**Nombre de alias**

Nombre (alias) que desee usar para hacer referencia a esta conexión.  

**Nombre de canalización** / **Número de puerto**  

Elementos adicionales de la cadena de conexión. El nombre de este cuadro varía según el protocolo seleccionado. Vea los temas enumerados a continuación para obtener ejemplos.  

**Protocolo**

Protocolo utilizado para la conexión.

**Server**

Nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que se va a conectar.  

## <a name="see-also"></a>Consulte también

- [Crear una cadena de conexión válida con el protocolo de memoria compartida](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
- [Crear una cadena de conexión válida con TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)
- [Crear una cadena de conexión válida con canalizaciones con nombre](/previous-versions/sql/sql-server-2016/ms189307(v=sql.130))