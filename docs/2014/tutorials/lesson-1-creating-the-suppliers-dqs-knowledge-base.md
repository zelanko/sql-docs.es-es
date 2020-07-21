---
title: 'Lección 1: crear la base de conocimiento de DQS proveedores | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 78825ccb-30fc-463c-8140-435532e2ecd2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e9421f568dae28895eb40b397d5e2589fafe0186
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054328"
---
# <a name="lesson-1-creating-the-suppliers-dqs-knowledge-base"></a>Lección 1: Creación de la base de conocimiento de DQS Proveedores
  En esta lección, creará una base de conocimiento de DQS denominada **Proveedores** con el conocimiento (los metadatos) sobre los datos de proveedor. Usará la base de conocimiento para realizar las actividades de limpieza y coincidencia sobre los datos de proveedor de entrada. La actividad de limpieza identifica los datos incorrectos o no válidos, corrige los datos incorrectos, propone correcciones y sugerencias, normaliza los datos y enriquece los datos con más información. La actividad de coincidencia compara los datos e identifica los registros similares (pero ligeramente diferentes) en los datos, lo que ayuda a quitar duplicados de los datos.  
  
 Se pueden usar procesos asistidos por PC y procesos interactivos para crear, compilar y administrar una base de conocimiento. El conocimiento de una base de conocimiento se mantiene en dominios, cada uno de los cuales es específico de un campo de los datos que desea limpiar o para los que desea buscar coincidencias.  
  
 En esta lección, realizará las tareas siguientes para crear la base de conocimiento **Proveedores** :  
  
-   Crear una base de conocimiento de DQS denominada **Proveedores**. Hay varias formas de crear una base de conocimiento. Puede crear una base de conocimiento desde el principio o puede crearla basándose en una base de conocimiento existente o importando un archivo de DQS (.dqs) que contiene una base de conocimiento creada previamente y exportada, o realizando una actividad de detección de conocimiento sobre los datos de ejemplo. En este tutorial, creará la base de conocimiento desde el principio.  
  
-   Crear dominios en la base de conocimiento **Proveedores** que usará para limpiar datos y para buscar coincidencias en los datos con el fin de identificar duplicados. Cree dominios para los campos de datos que desea usar en las actividades de limpieza y coincidencia, no para todos los campos de los datos.  
  
-   Agregar valores a un dominio agregando valores manualmente, importando valores de un archivo de Excel, realizando una actividad de detección de conocimiento sobre datos de ejemplo e importando valores de proyecto desde un proyecto de limpieza. También puede importar valores de dominio si importa un archivo de DQS que contiene propiedades y valores de dominio, pero no lo va a hacer en este tutorial.  
  
-   Establecer reglas para un dominio. Una regla de dominio es una condición que DQS emplea para validar, corregir y normalizar valores de dominio.  
  
-   Establecer relaciones basadas en términos para un dominio. Una relación basada en términos permite corregir términos que forman parte de los valores de un dominio. Por ejemplo, en el valor **Contoso Inc., Inc.** se puede definir un término como Incorporated. Esto ayuda a normalizar los datos y a identificar duplicados. Por ejemplo, **Contoso Inc.** y **Contoso Incorporated** se pueden considerar duplicados.  
  
-   Especificar sinónimos en valores de dominio. Puede establecer dos o más valores como sinónimos y establecer uno de ellos como valor inicial, que reemplaza sus valores de sinónimos durante una actividad de limpieza para normalizar los datos.  
  
-   Crear un dominio compuesto denominado Validación de direcciones que incluye los dominios Línea de dirección, Ciudad, Estado y Código postal. Un dominio compuesto es un dominio que consta de uno o varios dominios únicos. Permite crear una regla que afecta a varios dominios. Por ejemplo, puede definir una regla: si la ciudad es Los Ángeles, el estado debe ser CA, donde la ciudad y el son dominios independientes.  
  
-   Configurar y usar un servicio de datos de referencia. La característica Servicio de datos de referencia de Data Quality Services (DQS) le permite suscribirse a proveedores de datos de referencia terceros, y limpiar y enriquecer sus datos empresariales validándolos con los datos de alta calidad de dichos proveedores. Puede usar servicios de proveedores de DQS punteros desde DQS para normalizar, corregir o enriquecer los datos durante el proceso de limpieza. En este tutorial, aprenderá a configurar el entorno de DQS para usar un servicio de datos de referencia en Azure Marketplace y usar el servicio asociado al dominio compuesto validación de direcciones para limpiar los datos de dirección.  
  
-   Publicar la base de conocimiento para que se pueda usar en las actividades de limpieza y coincidencia.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 1: Creación de una base de conocimiento y dominios](../../2014/tutorials/task-1-creating-a-knowledge-base-and-domains.md)  
  
  
