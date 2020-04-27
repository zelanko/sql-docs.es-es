---
title: 'Propiedades del artículo: &lt;Artículo&gt; | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.articleproperties.f1
helpviewer_keywords:
- Article Properties dialog box
ms.assetid: 6dd601a4-1233-43d9-a9f0-bc8d84e5d188
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2903eef63152af9b2e9af1434ba12ea91b4058fc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62721787"
---
# <a name="article-properties---ltarticlegt"></a>Article Properties - &lt;Article&gt; (Propiedades del artículo: &lt;Artículo&gt;)
  El cuadro de diálogo **Propiedades del artículo** está disponible en el Asistente para nueva publicación y en el cuadro de diálogo **Propiedades de la publicación** . Le permite ver y establecer propiedades para todos los tipos de artículo. Algunas propiedades solo se pueden establecer cuando se crea la publicación, mientras que otras se pueden establecer únicamente si la publicación no tiene suscripciones activas. Las propiedades que no se pueden establecer se muestran como de solo lectura.  
  
> [!NOTE]  
>  Una vez creada una publicación, algunos cambios de las propiedades requieren una nueva instantánea. Si una publicación tiene suscripciones, algunos cambios también requieren reinicializar todas las suscripciones. Para obtener más información, vea [Cambiar las propiedades de la publicación y de los artículos](publish/change-publication-and-article-properties.md).  
  
 Cada propiedad del cuadro de diálogo **Propiedades del artículo** incluye una descripción. Al hacer clic en una propiedad, se muestra su descripción en la parte inferior del cuadro de diálogo. Este tema ofrece información adicional acerca de varias propiedades. Las propiedades se agrupan en las siguientes categorías:  
  
-   Propiedades que se aplican a todas las publicaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Propiedades que se aplican a las publicaciones transaccionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Propiedades que se aplican a las publicaciones de combinación.  
  
-   Propiedades que se aplican a las publicaciones transaccionales y de instantáneas de publicadores de Oracle.  
  
## <a name="options-for-all-publications"></a>Opciones para todas las publicaciones  
 **Copiar esquemas de particiones de tabla** y **Copiar esquemas de particiones de índice**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introdujo particiones de tabla y particiones de índice, que no están relacionadas con las ofertas de replicación de particiones a través de los filtros de fila y de columna. Las opciones **Copiar esquemas de particiones de tabla** y **Copiar esquemas de particiones de índice** especifican si los esquemas de particiones se deben copiar en el suscriptor. Para obtener más información acerca de las particiones, vea [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).  
  
 **Convertir tipos de datos**  
 Determina si se debe convertir desde tipos de datos definidos por el usuario a tipos de datos base cuando se crean objetos en el suscriptor. Los tipos de datos definidos por el usuario incluyen los tipos definidos por el usuario de CLR introducidos en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Especifique un valor **True** si se van a replicar estos tipos de datos con respecto a versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; de esta manera, se garantiza que se van a poder tratar correctamente en el suscriptor.  
  
 **Crear esquemas en el suscriptor**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introdujo esquemas que se definen mediante la instrucción CREATE SCHEMA. Un esquema es el propietario de un objeto; se usa en un nombre de varias partes, como por ejemplo \<Base de datos>.\<Esquema>.\<Objeto>. Si la base de datos tiene objetos que son propiedad de esquemas que no son DBO, la replicación puede crear estos esquemas en el suscriptor, de manera que se puedan crear objetos publicados.  
  
 Si se van a replicar datos en versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]:  
  
-   Establezca esta opción en **False**, ya que las versiones anteriores no son compatibles con CREATE SCHEMA.  
  
-   Para cada esquema, agregue un usuario a la base de datos de suscripciones con el mismo nombre que el esquema.  
  
 **Convertir XML a NTEXT**, **Convertir tipos de datos MAX a NTEXT e IMAGE**, **Convertir el tipo datetime nuevo a NVARCHAR**, **Convertir el tipo de secuencia de archivo a tipos de datos MAX**, **Convertir tipo CLR grande a tipos de datos MAX**, **Convertir tipo hierarchyId a tipos de datos MAX**y **Convertir tipo espacial a tipos de datos MAX**.  
 Determina si se deben convertir los tipos de datos y los atributos tal como se describe. Especifique un valor de **True** si va a replicar estos tipos de datos a versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De este modo, se garantiza que se administrarán correctamente en el suscriptor.  
  
 **Nombre del objeto de destino**  
 Nombre del objeto creado en la base de datos de suscripciones. Esta opción no se puede cambiar para artículos de publicaciones que están habilitadas para replicación transaccional punto a punto.  
  
 **Propietario del objeto de destino**  
 Esquema bajo el cual se crea el objeto en la base de datos de suscripciones. El valor predeterminado es el esquema al que pertenece el objeto en la base de datos de publicaciones, con las siguientes excepciones:  
  
-   Para artículos en publicaciones de combinación con un nivel de compatibilidad menor de 90: de manera predeterminada, el propietario se deja en blanco y se especifica como **dbo** durante la creación del objeto en el suscriptor.  
  
-   Para artículos de publicaciones de Oracle: de forma predeterminada, el propietario se especifica como **dbo**.  
  
-   Para artículos de publicaciones que utilizan instantáneas en modo de carácter (que se utilizan para los que no son suscriptores de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y para los suscriptores de [!INCLUDE[ssEW](../../includes/ssew-md.md)] ): de manera predeterminada, el propietario se deja en blanco. Como valor predeterminado del propietario se utiliza el propietario asociado con la cuenta utilizada por el Agente de distribución o el Agente de mezcla para conectarse con el suscriptor.  
  
 Esta opción no se puede cambiar para artículos de publicaciones que están habilitadas para replicación transaccional punto a punto.  
  
 **Administrar intervalos de identidad automáticamente**  
 La replicación, de manera predeterminada, administra todas las columnas de identidad en el publicador y en cada suscriptor. Cada nodo de replicación tiene asignado un intervalo de valores de identidad (que se especifica mediante las opciones **Tamaño de intervalo del publicador** y **Tamaño de intervalo del suscriptor** ) para garantizar que un valor dado se utilice únicamente en un nodo. Para más información, vea [Replicar columnas de identidad](publish/replicate-identity-columns.md).  
  
## <a name="options-for-transactional-publications"></a>Opciones para publicaciones transaccionales  
 **Copiar los procedimientos almacenados INSERT, UPDATE y DELETE**  
 Si, en la sección **Entrega de instrucción** de este cuadro de diálogo, selecciona utilizar los procedimientos almacenados para propagar cambios a los suscriptores (valor predeterminado), seleccione si se van a copiar los procedimientos en cada suscriptor. Si selecciona **False**, deberá copiar los procedimientos manualmente; de lo contrario, el Agente de distribución producirá un error al intentar entregar los cambios.  
  
 **Statement delivery**  
 Las opciones de esta sección se aplican a todas las tablas, incluidas las vistas indizadas que se replican como tablas. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda el uso de las opciones predeterminadas a menos que la aplicación requiera una funcionalidad diferente. De forma predeterminada, la replicación transaccional propaga los cambios a los suscriptores a través de una serie de procedimientos almacenados que se instalan en cada suscriptor. Cuando se produce una inserción, una actualización o una eliminación en una tabla del publicador, la operación se convierte en una llamada a un procedimiento almacenado en el suscriptor.  
  
 Las opciones de **Entrega de instrucción** especifican si se debe utilizar un procedimiento almacenado, y en ese caso, el formato que se debe utilizar para los parámetros que pasan al procedimiento. Las opciones de **Procedimiento almacenado** permiten utilizar los procedimientos que la replicación crea automáticamente o sustituir los procedimientos personalizados creados por el usuario.  
  
 Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 **Replicar**  
 Esta opción se aplica únicamente a los procedimientos de almacenamiento. Determina si se debe replicar la definición del procedimiento almacenado (instrucción CREATE PROCEDURE) o su ejecución. Si replica la ejecución del procedimiento, la definición del procedimiento se replica en el suscriptor cuando se inicializa la suscripción; cuando el procedimiento se ejecuta en el publicador, la replicación ejecuta el procedimiento correspondiente en el suscriptor. Esto puede mejorar notablemente el rendimiento para los casos en que se llevan a cabo grandes operaciones en lote. Para más información, vea [Publishing Stored Procedure Execution in Transactional Replication](transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
## <a name="options-for-merge-publications"></a>Opciones para publicaciones de combinación  
 El cuadro de diálogo **Propiedades del artículo** para las publicaciones de combinación tiene dos pestañas: **Propiedades** y **Solucionador**.  
  
### <a name="properties-tab"></a>Pestaña Propiedades  
 **Dirección de la sincronización**  
 Determina si los cambios se pueden cargar desde los suscriptores que utilizan el tipo de suscripción de cliente:  
  
-   **Bidireccional** (valor predeterminado): los cambios se pueden descargar en el suscriptor y cargar en el publicador.  
  
-   **Solo descargar en suscriptor y prohibir cambios del suscriptor**: los cambios pueden descargarse en el suscriptor, pero no pueden cargarse en el publicador. Los desencadenadores impiden que se realicen cambios en el suscriptor.  
  
-   **Solo descargar en suscriptor y permitir cambios del suscriptor**: los cambios pueden descargarse en el suscriptor, pero no pueden cargarse en el publicador.  
  
 Para más información, vea [Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga](merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Opciones de partición**  
 Especifica el tipo de particiones que crea un filtro con parámetros. Para obtener más información, vea la sección la sección sobre cómo establecer opciones de partición en el tema [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Nivel de seguimiento**  
 Determina si se deben tratar los cambios de la misma fila o columna como un conflicto.  
  
 **Comprobar permiso INSERT**, **Comprobar permiso UPDATE**y **Comprobar permiso DELETE**  
 Determina si se debe comprobar durante la sincronización que el inicio de sesión del suscriptor tenga permisos INSERT, UPDATE o DELETE en las tablas publicadas en la base de datos de publicaciones. El valor predeterminado es **False** porque la replicación de mezcla no requiere que se otorguen estos permisos; el acceso a las tablas publicadas se controla a través de la lista de acceso a la publicación (PAL). Para obtener más información sobre la PAL, vea [Secure the Publisher](security/secure-the-publisher.md) (Proteger el publicador).  
  
 Puede solicitar la comprobación de los permisos si desea permitir que uno o varios suscriptores carguen algunos cambios en los datos publicados, pero no otros. Por ejemplo, podría agregar un suscriptor a la PAL, pero sin otorgarle al suscriptor ningún permiso en las tablas de la base de datos de publicaciones. Entonces podría establecer la opción Comprobar permiso DELETE en **True**: el suscriptor podría cargar inserciones y actualizaciones, pero no eliminaciones.  
  
 **UPDATE en varias columnas**  
 Cuando la replicación de mezcla lleva a cabo una actualización, actualiza todas las columnas cambiadas en una instrucción UPDATE y restablece las columnas no modificadas a sus valores originales. La alternativa en estos casos es emitir múltiples instrucciones UPDATE, con una instrucción UPDATE para cada columna que ha sido modificada. La instrucción UPDATE en varias columnas normalmente es más eficaz, pero se debe analizar la posibilidad de establecer la opción en **False** si los desencadenadores de la tabla están establecidos para responder a las actualizaciones de determinadas columnas y responden de manera incorrecta porque tales columnas se restablecen cuando se llevan a cabo las actualizaciones.  
  
> [!IMPORTANT]  
>  Esta opción ha quedado desusada y se retirará en versiones posteriores.  
  
### <a name="resolver-tab"></a>Pestaña Solucionador  
 **Utilizar el solucionador predeterminado**  
 Si selecciona el solucionador predeterminado, los conflictos se resuelven sobre la base de la prioridad asignada a cada suscriptor o del primer cambio escrito en el publicador, en función del tipo de suscripciones utilizadas. Para más información, vea [Detectar y solucionar conflictos de replicación de mezcla](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 **Usar un solucionador personalizado (registrada en el distribuidor)**  
 Si opta por utilizar un solucionador de artículos (puede ser una proporcionado por [!INCLUDE[msCoName](../../includes/msconame-md.md)] o un escrito por el usuario), debe seleccionar un solucionador del cuadro de lista. Para más información, consulte [Replicación de mezcla avanzada: detección y resolución de conflictos](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 Si el solucionador requiere una entrada, especifíquela en el cuadro de texto **Especifique la información necesaria para el solucionador** . Para obtener más información acerca de la entrada requerida por los solucionadores personalizados de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , vea [Microsoft COM-Based Resolvers](merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 **Permitir que el suscriptor resuelva los conflictos de modo interactivo durante la sincronización a petición**  
 Seleccione esta opción si los suscriptores van a utilizar sincronización a petición (valor predeterminado para la replicación de mezcla) y desea solucionar conflictos de manera interactiva. Especifique la sincronización a petición en la página **Programación de sincronización** del Asistente para nueva suscripción. Para solucionar conflictos de manera interactiva, utilice la interfaz del usuario Solucionador interactivo. Para obtener más información, consulte [Interactive Conflict Resolution](merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
 **Solicitar comprobación de una firma digital antes de la mezcla**  
 Todos los solucionadores basados en COM proporcionados por [!INCLUDE[msCoName](../../includes/msconame-md.md)] están firmados. Seleccione esta opción para comprobar que el solucionador sea válido al sincronizar.  
  
## <a name="options-for-oracle-publications"></a>Opciones para las publicaciones de Oracle  
 El cuadro de diálogo **Propiedades del artículo** para las publicaciones de Oracle tiene dos pestañas: **Propiedades** y **Asignación de datos**. Las publicaciones de Oracle no admiten todas las propiedades admitidas por las publicaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para más información, consulte [Design Considerations and Limitations for Oracle Publishers](non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
### <a name="properties-tab"></a>Pestaña Propiedades  
 **Copiar los procedimientos almacenados INSERT, UPDATE y DELETE**  
 Si el artículo se encuentra en una publicación transaccional y, en la sección **Entrega de instrucción** de este cuadro de diálogo, selecciona utilizar los procedimientos almacenados para propagar cambios a los suscriptores (valor predeterminado), seleccione si se van a copiar los procedimientos en cada suscriptor. Si selecciona **False**, deberá copiar los procedimientos manualmente; de lo contrario, el Agente de distribución producirá un error al intentar entregar los cambios.  
  
 **Propietario del objeto de destino**  
 Si escribe un valor distinto de **dbo**:  
  
-   Para los suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior, debe garantizar la creación de un esquema en el suscriptor que tenga el mismo nombre que el valor que ha especificado. Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-schema-transact-sql).  
  
-   En el caso de los suscriptores que ejecutan versiones anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], para cada esquema, agregue un usuario a la base de datos de suscripciones con el mismo nombre que el esquema.  
  
 **Nombre de espacio de tablas**  
 Espacio de tablas en el cual se deben crear las tablas de seguimiento de cambios de replicación en la instancia del servidor de Oracle. Para más información, vea [Manage Oracle Databases](non-sql/manage-oracle-tablespaces.md) (Administrar bases de datos de Oracle).  
  
 **Statement delivery**  
 Las opciones de esta sección se aplican a todas las tablas de publicaciones transaccionales. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda el uso de las opciones predeterminadas a menos que la aplicación requiera una funcionalidad diferente. De forma predeterminada, la replicación transaccional propaga los cambios a los suscriptores a través de una serie de procedimientos almacenados que se instalan en cada suscriptor. Cuando se produce una inserción, una actualización o una eliminación en una tabla del publicador, la operación se convierte en una llamada a un procedimiento almacenado en el suscriptor.  
  
 Las opciones de **Entrega de instrucción** especifican si se debe utilizar un procedimiento almacenado, y en ese caso, el formato que se debe utilizar para los parámetros que pasan al procedimiento. Las opciones de **Procedimiento almacenado** permiten utilizar los procedimientos que la replicación crea automáticamente o sustituir los procedimientos personalizados creados por el usuario.  
  
 Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
### <a name="data-mapping-tab"></a>Pestaña Asignación de datos  
 **Nombre de la columna**  
 Nombre de la columna en el publicador (solo lectura).  
  
 **Tipo de datos del publicador**  
 Tipo de datos de Oracle para la columna en el publicador (solo lectura). El tipo de datos solamente se puede cambiar directamente en la base de datos de Oracle. Para obtener más información, vea la documentación de Oracle.  
  
 **Tipo de datos del suscriptor**  
 Tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que se asigna el tipo de datos de Oracle cuando se replican los datos:  
  
-   Para algunos tipos de datos, solo hay una asignación posible, en cuyo caso la columna de la cuadrícula de propiedades es de solo lectura.  
  
-   Para algunos tipos, hay más de un tipo que puede seleccionar. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda el uso de la asignación predeterminada a menos que la aplicación requiera una asignación diferente. Para más información, consulte [Data Type Mapping for Oracle Publishers](non-sql/data-type-mapping-for-oracle-publishers.md).  
  
## <a name="see-also"></a>Consulte también  
 [Create a Publication](publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](publish/view-and-modify-publication-properties.md)   
 [Crear y aplicar la instantánea inicial](create-and-apply-the-initial-snapshot.md)   
 [Reinicializar una suscripción](reinitialize-a-subscription.md)   
 [Publicar datos y objetos de base de datos](publish/publish-data-and-database-objects.md)  
  
  
