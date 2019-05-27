---
title: La configuración de red del clúster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- cluster network selection, Setup
- cluster network selection
ms.assetid: 579482ef-a023-45b2-9176-b4a4188adf9d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48dca8e9ce522f2520521441b2e7eea349ff099b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096436"
---
# <a name="cluster-network-configuration"></a>Configuración de red en clúster
  Utilice la página **Selección de red en clúster** para especificar los recursos de red para la instancia en clúster de conmutación por error.  
  
## <a name="options"></a>Opciones  
 **Nombre de red en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: es el nombre usado para identificar la instancia del clúster de conmutación por error en la red.  
  
 **Configuración de red**: especifique el tipo de IP y la dirección IP de la instancia del clúster de conmutación por error.  
  
 Durante las operaciones Agregar nodo y Quitar nodo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra una lista de solo lectura de las direcciones IP existentes para el clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Instalación integrada:  
  
    -   Si va a agregar un nodo que admita un conjunto idéntico de subredes de red que admitan los nodos existentes del clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no se puede agregar ninguna dirección IP adicional. La configuración de dependencia permanece sin modificar.  
  
    -   Si va a agregar un nodo que admita un subconjunto de las subredes de red que admitan los nodos existentes en el clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no se pueden agregar recursos de dirección IP adicionales. La dependencia de recursos de direcciones IP se establece en OR para reflejar que todas las direcciones IP especificadas no son válidas en todos los nodos de clúster.  
  
    -   Si va a agregar un nodo que admita subredes además de las subredes que ya admitían los nodos existentes en el clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tiene la opción de agregar nuevas direcciones IP válidas. Si se especifican nuevas direcciones IP, la dependencia de recursos de direcciones IP se establece en OR para reflejar que todas las direcciones IP especificadas no son válidas en todos los nodos de clúster.  
  
    -   Si va a agregar un nodo que sea compatible con subredes de red adicionales, pero no es compatible con ninguna de las subredes admitidas por los nodos existentes en el clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tiene que agregar más direcciones IP. La dependencia de recursos de direcciones IP se establece en OR para reflejar que todas las direcciones IP especificadas no son válidas en todos los nodos de clúster.  
  
-   Instalación avanzada: Durante el paso completo de la instalación, especifique la dirección IP para todos los nodos y subredes de la instancia de clúster de conmutación por error. Puede especificar varias direcciones IP para un clústeres de conmutación por error de varias subredes, pero solo se admite una dirección IP por subred. Cada nodo preparado debe ser propietario de al menos una dirección IP. Si tiene varias subredes en su clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] m se le solicitará que establezca la dependencia de recursos de dirección IP en OR. Quitar nodo:  
  
    -   Si el resto de direcciones IP se admite en los nodos restantes, se le pide que establezca la dependencia de recursos de dirección IP en AND.  
  
    -   Si el resto de direcciones IP no se admiten en todos los nodos restantes, la dependencia de recursos de dirección IP se deja como OR.  
  
  
