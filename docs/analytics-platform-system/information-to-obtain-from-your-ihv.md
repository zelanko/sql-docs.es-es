---
title: Obtener información de IHV
description: Información que se va a obtener de su IHV sobre el dispositivo de sistema de la plataforma de análisis.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 730cf09ab7e45ea74070db591592fdb871243a77
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401065"
---
# <a name="information-to-obtain-from-your-ihv"></a>Información que se debe obtener de su IHV
Cuando su proveedor de hardware independiente (IHV) le entregue su nuevo PDW de SQL Server dispositivo, también proporcionará información sobre el hardware del dispositivo y la configuración que han realizado en el dispositivo. Necesitará esta información para administrar el dispositivo.  
  
En la lista siguiente se muestra información que suele ser necesaria desde el IHV. En algunos casos, se necesita información adicional o de otro. Consulte con el IHV para asegurarse de que toda la información relevante se le ha transferido con la entrega del dispositivo.  
  
|||  
|-|-|  
|**Información o documento**|**Descripción**|  
|Lista de materiales (BOM)|En su lista de materiales se enumeran los componentes que se incluyen en el dispositivo. Esta información es necesaria para confirmar que se han entregado todos los componentes.<br /><br />**Importante:** La lista de materiales debe incluir pesos para cada uno de los nodos del dispositivo y para cada bastidor completo. Esta información es importante a la hora de planear cómo controlar y trasladar componentes del dispositivo, y para asegurarse de que el centro de datos puede alojar el dispositivo. Si la marca BOM no incluye pesos de nodo, asegúrese de obtener esta información de su IHV para todos los nodos.|  
|Diagramas de cableado|Los diagramas de cableado muestran cómo conectar la red, la alimentación y otros cables para cada bastidor del dispositivo. Estos diagramas son necesarios cuando se instala el dispositivo en el centro de datos y cada vez que se necesita quitar o reemplazar un componente.|  
|Requisitos de montaje en bastidor del dispositivo|Antes de que el dispositivo pueda instalarse en el centro de datos, debe saber si el centro de datos cumple los requisitos de flujo de aire y de longitud de cable para el dispositivo, así como los requisitos de tamaño y energía de los componentes. Consulte también la lista de materiales (BOM) anterior para obtener información sobre las ponderaciones de los componentes del dispositivo, que también es necesaria.|  
  
