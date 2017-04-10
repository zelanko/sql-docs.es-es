---
title: "Generar autom&#225;ticamente un conjunto de filtros de combinaci&#243;n entre art&#237;culos de mezcla (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "generación automática de filtro de combinación"
  - "filtros de combinación"
ms.assetid: 7ef419f4-c17f-42a5-9068-174a3ec08941
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Generar autom&#225;ticamente un conjunto de filtros de combinaci&#243;n entre art&#237;culos de mezcla (SQL Server Management Studio)
  Generar automáticamente un conjunto de filtros de combinación en el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Si genera automáticamente un conjunto de filtros de combinación en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo después de han inicializado las suscripciones a la publicación, debe generar una nueva instantánea y reinicializar todas las suscripciones después de realizar el cambio. Para obtener más información acerca de los requisitos para los cambios de propiedad, vea [Propiedades de artículo y publicación de cambio](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
 Es posible crear filtros de combinación para un conjunto de tablas de forma manual, o bien la replicación puede generar los filtros de forma automática en función de las relaciones de clave clave externa a clave principal definidas en las tablas. Para obtener más información acerca de cómo crear filtros de combinación manualmente, consulte [definir y modificar una combinación filtro entre combinar artículos](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
### Para generar automáticamente un conjunto de filtros de combinación entre artículos de mezcla  
  
1.  En el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>**, haga clic en **Agregar**, y, a continuación, haga clic en **Generar filtros automáticamente**.  
  
    > [!NOTE]  
    >  Al generar filtros automáticamente, se eliminan los filtros de fila o los filtros de combinación existentes en la publicación. Es posible agregar filtros después de haber generado automáticamente un conjunto de filtros.  
  
2.  Siga el proceso del cuadro de diálogo **Generar filtros** para crear un filtro de fila. A continuación, el filtro de fila se amplía a las tablas relacionadas con la tabla filtrada por medio de las relaciones de clave principal y clave externa.  
  
    1.  Seleccione una tabla para filtrar en la lista desplegable.  
  
    2.  Cree una instrucción para el filtro en el cuadro de texto **Instrucción de filtro** . Puede escribir directamente en el área de texto o puede arrastrar y colocar columnas del cuadro de lista **Columnas** .  
  
         El área de texto **Instrucción de filtro** incluye el texto predeterminado, que tiene este formato:  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
         El texto predeterminado no se puede modificar; escriba la cláusula de filtro para un filtro de fila estático o un filtro de fila con parámetros después de la palabra clave WHERE mediante la sintaxis SQL estándar. La cláusula de filtro completa para un filtro de fila con parámetros sería similar a la siguiente:  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         La cláusula WHERE debe usar nombres de dos partes; los nombres de tres y cuatro partes no se admiten.  
  
    3.  Especifique las opciones del filtro.  
  
         Seleccione la opción que coincida con el modo en que se van a compartir los datos entre suscriptores: **Una fila de esta tabla irá a varias suscripciones** o **Una fila de esta tabla irá a una sola suscripción**. Si selecciona **Una fila de esta tabla irá a una sola suscripción**, la replicación de mezcla puede optimizar el rendimiento almacenando y procesando menos metadatos. No obstante, debe asegurarse de que los datos se particionan de forma que una fila no se pueda replicar en más de un suscriptor. Para obtener más información, vea la sección sobre cómo configurar opciones de partición en el tema [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     El filtro que ha especificado se analiza y se ejecuta según la tabla de la cláusula SELECT. Si la instrucción de filtro contiene errores de sintaxis u otros problemas, se le notificará y podrá modificar dicha instrucción.  
  
     Una vez analizada la instrucción, la replicación crea los filtros de combinación necesarios y los muestra en el panel **Tablas filtradas** de la página **Filtrar filas de tabla** o **Filtrar filas** . Si genera filtros desde el Asistente para nueva publicación y aún no ha configurado el distribuidor para el publicador en el que se ejecuta este asistente, se le pedirá que lo haga.  
  
4.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
### Para modificar un filtro generado automáticamente  
  
1.  En el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>**, seleccione un filtro en el **tablas filtradas** panel y, a continuación, haga clic en **Editar**.  
  
2.  En el cuadro de diálogo **Editar filtro** o **Editar combinación** , modifique el filtro.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para eliminar un filtro generado automáticamente  
  
1.  En el **filtrar filas de tabla** página del Asistente para nueva publicación o **filtrar filas** página de la **Propiedades de la publicación - \< publicación>**, seleccione un filtro en el **tablas filtradas** panel y, a continuación, haga clic en **Eliminar**.  
  
## Vea también  
 [Filtros de combinación](../../../relational-databases/replication/merge/join-filters.md)   
 [Filtros de fila con parámetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  