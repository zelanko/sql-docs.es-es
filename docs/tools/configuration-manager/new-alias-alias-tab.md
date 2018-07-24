---
title: Nuevo Alias (pestaña Alias) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 785eb6fb-f67e-449d-b1c8-c38dfbb95ef6
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31a5d53060a892ac55a9e040e9c54d57e3da1f4e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37995097"
---
# <a name="new-alias-alias-tab"></a>Nuevo alias (pestaña Alias)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Un alias es un nombre alternativo que se puede utilizar para establecer una conexión. El alias encapsula los elementos necesarios de una cadena de conexión y los expone con un nombre elegido por el usuario. Use la página **Alias** del cuadro de diálogo **Alias - Nuevo** para especificar los elementos de la cadena de conexión de un alias. Para cambiar la cadena de conexión de un alias existente, vea [Propiedades de &#60;Alias&#62; &#40;pestaña Alias&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md).  
  
 No es necesario completar todos los valores de la cuadrícula **Propiedades** . Las combinaciones válidas varían en función del protocolo seleccionado. Vea los temas enumerados abajo para obtener ejemplos de combinaciones válidas.  
  
 **Nombre de alias**  
 Nombre (alias) que desee usar para hacer referencia a esta conexión.  
  
 **Nombre de canalización** / **Número de puerto**  
 Elementos adicionales de la cadena de conexión. El nombre de este cuadro varía según el protocolo seleccionado.  
  
 **Protocolo**  
 Protocolo utilizado para la conexión.  
  
 **Server**  
 Nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que se va a conectar.  
  
## <a name="when-to-use-an-alias"></a>Cuándo utilizar un alias  
 De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta a una instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el protocolo **Memoria compartida** y a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en otro equipo mediante **TCP/IP** o **Canalizaciones con nombre**. Cree un alias cuando use TCP/IP o canalizaciones con nombre y desee proporcionar una cadena de conexión personalizada; o bien, cuando desee usar un nombre distinto del nombre de servidor para la conexión.  
  
### <a name="examples"></a>Ejemplos  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no escucha en el puerto TCP/IP predeterminado 1433, por lo que querrá proporcionar una cadena de conexión con otro número de puerto.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no escucha en la canalización con nombre predeterminada, por lo que desea proporcionar una cadena de conexión con una canalización con nombre diferente.  
  
-   Una aplicación espera conectarse a una base de datos en el servidor llamado `ACCT`, pero la base de datos se ha consolidado como una instancia con el nombre `ACCT` en un servidor llamado `CENTRAL`. La aplicación no se puede modificar de forma sencilla. Cree un alias llamado `ACCT`, con una cadena de conexión que apunte a `CENTRAL\ACCT`.  
  
## <a name="creating-a-valid-connection-string"></a>Crear una cadena de conexión válida  
 Vea los siguientes temas para obtener una descripción y ejemplos de combinaciones válidas de propiedades de alias:  
  
-   [Crear una cadena de conexión válida con el protocolo de memoria compartida](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
-   [Crear una cadena de conexión válida con TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)  
  
-   [Crear una cadena de conexión válida con canalizaciones con nombre](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)  
  
  
