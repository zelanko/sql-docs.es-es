---
title: Conceptos básicos de ADO | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54e829ed3c28702144c64c49a9bd425e6488e5d7
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="ado-fundamentals"></a>Conceptos básicos de ADO
ADO ofrece a los desarrolladores un modelo de objetos eficaces y lógica para el acceso mediante programación, editar y actualizar los datos desde una gran variedad de orígenes de datos a través de interfaces del sistema de OLE DB. El uso más común de ADO es consultar una o varias tablas en una base de datos relacional, recuperar y mostrar los resultados en una aplicación y es posible que los usuarios puedan hacer y guardar los cambios en los datos. Otras tareas son los siguientes:  
  
-   Consultar una base de datos mediante SQL y mostrar los resultados.  
  
-   Acceso a la información en un almacén de archivos a través de Internet.  
  
-   Manipular mensajes y carpetas en un sistema de correo electrónico.  
  
-   Guardar datos de una base de datos en un archivo XML.  
  
-   Ejecutar comandos que se describen con XML y recuperar una secuencia XML.  
  
-   Guardar datos en una secuencia binaria o XML.  
  
-   Permitir que un usuario revisar y cambiar datos en tablas de base de datos.  
  
-   Crear y volver a parametrizar los comandos de base de datos.  
  
-   Ejecutar procedimientos almacenados.  
  
-   Crear dinámicamente una estructura flexible, que se denomina un **Recordset**, para contener, navegar y manipular los datos.  
  
-   Realizar operaciones de base de datos transaccional.  
  
-   Filtrar y ordenar copias locales de información de base de datos basándose en criterios de tiempo de ejecución.  
  
-   Crear y manipular resultados jerárquicos de bases de datos.  
  
-   Campos de base de datos de enlace para los componentes dependientes de datos.  
  
-   Crear desconectados remotos **conjuntos de registros**.  
  
 ADO expone una amplia variedad de opciones y configuración para proporcionar esta flexibilidad. Por lo tanto, es importante seguir un enfoque metódico para aprender a utilizar ADO en una aplicación, descomponiendo cada uno de los objetivos en partes manejables.  
  
 Cuatro operaciones principales implicadas en la mayoría de las aplicaciones que utilicen ADO: obtener datos, examinar los datos, editar datos y actualizar datos. Estas operaciones se examinan con más detalle más adelante en esta sección.  
  
 Sin embargo, antes de describir estos detalles, se presentará información general sobre el modelo de objetos ADO y una aplicación ADO simple, que está escrita en Microsoft® Visual Basic® y realiza cada una de las cuatro operaciones principales de ADO:  
  
-   [Colecciones y los objetos ADO](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData: Una aplicación ADO Simple](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [Proveedores OLE DB](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [Errores](../../../ado/guide/data/errors-ado.md)
