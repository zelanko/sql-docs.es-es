---
title: Obtener información de IHV - Analytics Platform System | Documentos de Microsoft
description: Información para obtener de su IHV sobre el dispositivo de sistema de la plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 57b61ed7741bc6d36b7531a62416893e7cc10fb7
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538905"
---
# <a name="information-to-obtain-from-your-ihv"></a>Información para obtener de su IHV
Cuando el proveedor de hardware independientes (IHV) proporciona el nuevo dispositivo PDW de SQL Server al usuario, también ofrecerá información sobre el hardware del equipo y la configuración que han llevado a cabo en el dispositivo. Necesitará esta información para administrar el dispositivo.  
  
En la lista siguiente muestra la información que normalmente es necesario desde el IHV. En algunos casos, es necesario adicional u otra información. Póngase en contacto con el IHV para asegurarse de que toda la información pertinente se ha transferido a la con la entrega de dispositivo.  
  
|||  
|-|-|  
|**Información o documento**|**Description**|  
|Lista de materiales (l. MAT)|La lista de materiales se enumeran los componentes que se incluyen en el dispositivo. Esta información es necesaria confirmar que todos los componentes se enviaron.<br /><br />**Importante:** la lista de materiales debe incluir pesos para cada uno de los nodos de dispositivo y para cada bastidor completa. Esta información es importante al planear cómo administrar y mover los componentes de dispositivo, y para asegurarse de su centro de datos puede dar cabida a la aplicación. Si la lista de materiales no incluye los pesos de nodo, asegúrese de obtener esta información desde su IHV para todos los nodos.|  
|Diagramas de cableado|Diagramas de cableado muestran cómo conectarse a la red, cables de alimentación y otros para cada dispositivo de bastidor. Estos diagramas son necesarios al instalar el dispositivo en su centro de datos, y siempre que necesite quitar o sustituir un componente.|  
|Requisitos de bastidor de tipo de dispositivo|Para poder instalar el dispositivo en su centro de datos, debe saber si su centro de datos cumple el flujo de aire y requisitos de longitud de cable para el dispositivo, así como el tamaño y los requisitos de energía para los componentes. Consulte también lista de materiales (l. MAT) anteriormente para obtener información acerca de los pesos de componente de aplicación, que también es necesario.|  
  
