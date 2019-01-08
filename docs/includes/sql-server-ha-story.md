En este artículo se ofrece una visión global de las soluciones de continuidad empresarial para alta disponibilidad y recuperación ante desastres en SQL Server. 

Una tarea habitual que todo usuario que implemente SQL Server debe tener en cuenta es la comprobación de que todas las instancias de SQL Server críticas y las bases de datos que contienen están disponibles en el momento en que el negocio y los usuarios finales las necesitan; ya sea de 9 a 5 o durante todo el día. El objetivo es mantener la empresa en funcionamiento con una interrupción mínima o inexistente. Este concepto se conoce también como continuidad empresarial.

SQL Server 2017 presenta muchas características nuevas o mejoras a las ya existentes, algunas de las cuales están relacionadas con la disponibilidad. La novedad más importante en SQL Server 2017 es la compatibilidad con SQL Server en las distribuciones de Linux. Para obtener una lista completa de las nuevas características de SQL Server 2017, vea el tema [Novedades de SQL Server 2017](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2017).

En este artículo se tratan principalmente los escenarios de disponibilidad de SQL Server 2017, así como las características de disponibilidad nuevas y mejoradas en SQL Server 2017. Entre estos escenarios se encuentra los híbridos que pueden contener implementaciones de SQL Server en Windows Server y Linux, así como los que pueden aumentar el número de copias que se pueden leer de una base de datos. Si bien este artículo no trata las opciones de disponibilidad externas a SQL Server, como aquellas que proporciona la virtualización, todo lo que se analiza aquí se aplica a las instalaciones de SQL Server que se encuentran dentro de una máquina virtual invitada, ya sea en la nube pública u hospedada por un servidor hipervisor no local.

## <a name="sql-server-2017-scenarios-using-the-availability-features"></a>Escenarios de SQL Server 2017 que utilizan las características de disponibilidad

Los grupos de disponibilidad, las FCI y los trasvases de registros pueden utilizarse de diferentes maneras, y no necesariamente solo con fines de disponibilidad. Son cuatro las formas principales en que se pueden utilizar las características de disponibilidad:

* Alta disponibilidad
* Recuperación ante desastres
* Migraciones y actualizaciones
* Escalado horizontal de copias legibles de una o varias bases de datos

En cada sección se describe las características pertinentes que se pueden usar para ese escenario concreto. La única característica que no se trata aquí es la [replicación de SQL Server](https://docs.microsoft.com/sql/relational-databases/replication/sql-server-replication). Aunque oficialmente no se ha designado como una característica de disponibilidad bajo el concepto genérico AlwaysOn, se utiliza a menudo para hacer los datos redundantes en determinados escenarios. La replicación se agregará a SQL Server en Linux en una versión futura.

> [!IMPORTANT] 
> Las características de disponibilidad de SQL Server no implican que se pueda prescindir de una estrategia de coopta de seguridad eficiente y bien probada, ya que este es el bloque de creación más fundamental de cualquier solución de disponibilidad.

### <a name="high-availability"></a>Alta disponibilidad

Es importante asegurarse de que las instancias o la base de datos de SQL Server están disponibles en caso de que se produzca un problema en un centro de datos o una única región en la región de la nube. En esta sección se explica cómo pueden ser de utilidad las características de disponibilidad para realizar esa tarea. Todas las características descritas están disponibles tanto en Windows Server como en Linux. 

#### <a name="always-on-availability-groups"></a>Grupos de disponibilidad AlwaysOn

Introducidos en SQL Server 2012, los Grupos de disponibilidad AlwaysOn (grupos de disponibilidad) proporcionan protección a nivel de base de datos mediante el envío de cada transacción de una base de datos a otra instancia, conocida como una réplica, que contiene una copia de esa base de datos en un estado especial. Es posible implementar un grupo de disponibilidad en las ediciones Standard o Enterprise.  Las instancias que participan en un grupo de disponibilidad pueden ser instancias independiente o instancias de clúster de conmutación por error de AlwaysOn (FCI, se describen en la siguiente sección). Puesto que las transacciones se envían a una réplica en el momento en que se producen, los grupos de disponibilidad están recomendados en aquellos casos en que se requiere un punto de recuperación y objetivos de tiempo de recuperación inferiores. El movimiento de datos entre las réplicas puede ser sincrónico o asincrónico; en el caso de la versión Enterprise Edition, se permiten hasta tres réplicas (incluida la principal) como sincrónicas. Un grupo de disponibilidad tiene una copia de lectura/escritura completa de la base de datos que se encuentra en la réplica principal, mientras que todas las réplicas secundarias no pueden recibir transacciones directamente de los usuarios finales o las aplicaciones. 

> [!NOTE] 
> AlwaysOn es un término genérico para las características de disponibilidad de SQL Server y abarca tanto los grupos de disponibilidad como los FCI. AlwaysOn no es el nombre de la característica del grupo de disponibilidad.

Dado que los grupos de disponibilidad solo proporcionan protección a nivel de base de datos, y no a nivel de instancia, cualquier elemento no capturado en el registro de transacciones o no configurado en la base de datos tendrá que sincronizarse manualmente para cada réplica secundaria. Algunos ejemplos de objetos que se deben sincronizar manualmente son los inicios de sesión a nivel de instancia, los servidores vinculados y los trabajos del Agente SQL Server.

Un grupo de disponibilidad también tiene otro componente denominado el agente de escucha, que permite a las aplicaciones y los usuarios finales conectarse sin necesidad de conocer qué instancia de SQL Server hospeda la réplica principal. Cada grupo de disponibilidad tendrá su propio agente de escucha. Si bien las implementaciones del agente de escucha son ligeramente diferentes en Windows Server y Linux, la funcionalidad que ofrece y el modo en que se utiliza son iguales. La figura siguiente muestra un grupo de disponibilidad basado en Windows Server que está usando un clúster de conmutación por error de Windows Server (WSFC). Se requiere un clúster subyacente en el nivel de sistema operativo para la disponibilidad, ya sea en Linux o en Windows Server. En el ejemplo se muestra una sencilla configuración de dos servidores, o nodos, en la que el WSCF es el clúster subyacente. 

![Grupo de disponibilidad sencillo](media/sql-server-ha-story/image1.png)
 
Las versiones Standard y Enterprise Edition tienen diferentes valores máximos diferentes en lo relativo a las réplicas. Un grupo de disponibilidad en Standard Edition, conocido como Grupo de disponibilidad básica, admite dos réplicas (una principal y otra secundaria) con una sola base de datos en el grupo de disponibilidad. La versión Enterprise Edition no solo permite que se configuren varias bases de datos en un solo grupo de disponibilidad, sino que también puede tener hasta nueve réplicas totales (una principal, ocho secundarias). Enterprise Edition también proporciona otras ventajas opcionales, como las réplicas secundarias legibles o la posibilidad de realizar copias de seguridad a partir de una réplica secundaria, entre otras.

>[!NOTE]
> La creación de reflejo de la base de datos, que se quedó en desuso en SQL Server 2012, no está disponible en la versión de Linux de SQL Server ni se agregará. Los usuarios que aún utilizan la creación de reflejo de la base de datos deben empezar a planear la migración a grupos de disponibilidad, que son lo que sustituye a la creación de reflejo de la base de datos.

En cuanto a la disponibilidad, los grupos de disponibilidad pueden proporcionar conmutación por error automática o manual. La conmutación automática por error puede producirse si se configura el movimiento de datos sincrónico y la base de datos en la réplica principal y secundaria se encuentra en un estado sincronizado. Siempre que se utilice el agente de escucha y la aplicación haga uso de una versión posterior de .NET (3.5 con una actualización, o 4.0 y versiones posteriores), la conmutación por error debe controlarse con una repercusión mínima o nula en los usuarios finales en caso de que se utilice un agente de escucha. La conmutación por error para convertir la réplica secundaria en la nueva réplica principal puede configurarse para que sea automática o manual, y generalmente se mide en segundos.

La lista siguiente resalta algunas diferencias con los grupos de disponibilidad en Windows Server y Linux:
* Debido a diferencias en el funcionamiento del clúster subyacente en Linux y Windows Server, todas las conmutaciones por error (manuales o automáticas) de los grupos de disponibilidad se realizan a través del clúster en Linux. En implementaciones de grupos de disponibilidad basadas en Windows Server, las conmutaciones por error manuales deben hacerse a través de SQL Server. Las conmutaciones automáticas por error se controlan mediante el clúster subyacente en Windows Server y Linux. 
* En SQL Server 2017, la configuración recomendada para los grupos de disponibilidad en Linux será como mínimo de tres réplicas. Esto se debe a la manera en que funciona la agrupación en clústeres subyacente. Después del lanzamiento se publicará una solución mejorada para una configuración de dos réplicas.
* En Linux, el nombre común usado por cada agente de escucha se define en DNS y no en el clúster, como ocurre en Windows Server.

En SQL Server 2017, hay algunas nuevas características y mejoras para los grupos de disponibilidad:

* Tipos de clúster
* REQUIRED_SECONDARIES_TO_COMMIT
* Compatibilidad mejorada del Coordinador de transacciones distribuidas (DTC) para las configuraciones basadas en Windows Server
* Escenarios adicionales de escalado horizontal para bases de datos de solo lectura (descritas más adelante en este artículo)

##### <a name="always-on-availability-group-cluster-types"></a>Tipos de clúster de grupo de disponibilidad AlwaysOn

La forma de disponibilidad integrada de agrupación en clústeres de Windows Server se habilita a través de una característica denominada Clústeres de conmutación por error. Permite crear un WSFC para su uso con un grupo de disponibilidad o FCI. La integración para los grupos de disponibilidad y las FCI se proporciona mediante los archivos DLL de recursos dependientes del clúster que proporciona SQL Server. 

Cada distribución de Linux compatible distribuye su propia versión de la solución de clúster Pacemaker. SQL Server 2017 en Linux es compatible con el uso de Pacemaker. Pacemaker es una solución de pila abierta que cada distribución puede integrar con su pila. Aunque las distribuciones incluyen Pacemaker, la aplicación no está tan integrada como la característica Clústeres de conmutación por error en Windows Server.

Un clúster WSFC y Pacemaker se parecen más de lo que se diferencian. Ambos proporcionan una manera de aprovechar los servidores individuales y combinarlos en una configuración para proporcionar disponibilidad, y tienen conceptos de elementos como recursos, restricciones (incluso si se implementan de manera diferente), conmutación por error, etc. A fin de que Pacemaker se admita tanto en configuraciones de grupo de disponibilidad como de FCI, incluyendo aspectos como la conmutación automática por error, Microsoft proporciona el paquete mssql-server-ha para Pacemaker que ,aunque es parecido, no es exactamente igual a los DLL del recurso en un clúster WSFC. Una de las diferencias entre un clúster WSFC y Pacemaker es que no hay ningún recurso de nombre de red en Pacemaker, que es el componente que ayuda a tomar el nombre del agente de escucha (o el nombre de la FCI) en un clúster WSFC. DNS proporciona la resolución de nombres en Linux.

Debido a la diferencia en la pila de clúster, se necesitan algunos cambios para los grupos de disponibilidad porque SQL Server tiene que controlar algunos de los metadatos que se controlan de forma nativa por un clúster WSFC. El mayor [!IMPORTANT] cambio es la introducción de un tipo de clúster para un grupo de disponibilidad. Está almacenado en sys.availability_groups en las columnas cluster_type y cluster_type_desc. Hay tres tipos de clústeres:

* WSFC 
* External
* None

Todos los grupos de disponibilidad que necesitan disponibilidad deben utilizar un clúster subyacente, lo que en el caso de SQL Server 2017 significa un clúster WSFC o Pacemaker. Para los grupos de disponibilidad basados en Windows Server que usan un clúster WSFC subyacente, el tipo de clúster predeterminado es WSFC (y no es necesario configurarlo). Para los grupos de disponibilidad basados en Linux, al crear el grupo de disponibilidad, el tipo de clúster debe establecerse como Externo. La integración con Pacemaker se configura después de crear el grupo de disponibilidad, mientras que en un clúster de WSFC esto se hace en el momento de la creación.

El tipo de clúster Ninguno puede utilizarse con grupos de disponibilidad de Windows Server y Linux. La configuración del tipo de clúster en Ninguno implica que el grupo de disponibilidad no requiere un clúster subyacente. Esto significa que SQL Server 2017 es la primera versión de SQL Server que admite grupos de disponibilidad sin un clúster, pero el inconveniente es que esta configuración no se admite como solución de alta disponibilidad. 

> [!IMPORTANT] 
> SQL Server 2017 no permite cambiar un tipo de clúster para un grupo de disponibilidad una vez que se ha creado. Esto significa que un grupo de disponibilidad no puede cambiarse de Ninguno a Externo o WSFC, o viceversa. 

Para aquellos usuarios que simplemente desean agregar otras copias de solo lectura de una base de datos o desean disfrutar de la misma funcionalidad que proporciona un grupo de disponibilidad para migración/actualizaciones, pero sin la complejidad adicional que implica un clúster subyacente o incluso una replicación, un grupo de disponibilidad con un tipo de clúster Ninguno es una solución perfecta. Para más información, vea las secciones [Migraciones y actualizaciones](#Migrations) y [Escalado de lectura](#ReadScaleOut). 

La captura de pantalla siguiente muestra la compatibilidad para los distintos tipos de tipos de clúster en SSMS. Debe ejecutar la versión 17.1 o una posterior. La captura de pantalla siguiente es de la versión 17.2.

![Opciones de AG de SSMS](media/sql-server-ha-story/image2.png)
 
##### <a name="requiredsynchronizedsecondariestocommit"></a>REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT

SQL Server 2016 aumentó la compatibilidad para el número de réplicas sincrónicas de dos a tres en la versión Enterprise Edition. Sin embargo, si se sincronizaba una réplica secundaria pero la otra experimentaba un problema, no existía ningún modo de controlar el comportamiento a fin de indicar a la principal que esperase a la réplica que tenía un comportamiento inadecuado o que le permitiera continuar. Esto significa que la réplica principal en algún momento seguiría recibiendo tráfico de escritura, incluso si la réplica secundaria no estuviera en estado sincronizado, con lo que se produciría una pérdida de datos en la réplica secundaria.
SQL Server 2017 incluye ahora una opción que permite controlar el comportamiento de lo que sucede cuando hay réplicas sincrónicas denominada REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT. La opción funciona como se describe a continuación:
* Hay tres valores posibles: 0, 1 y 2
* El valor es el número de réplicas secundarias que deben sincronizarse, lo cual tiene implicaciones para la pérdida de datos, la disponibilidad del grupo de disponibilidad y la conmutación por error.
* En el caso de los clústeres WSFC y el tipo de clúster Ninguno, el valor predeterminado es 0 y se puede establecer manualmente en 1 o 2.
* Para un tipo de clúster Externo, el mecanismo del clúster configurará esta opción de manera predeterminada, aunque puede reemplazarse manualmente. Para tres réplicas sincrónicas, el valor predeterminado será 1.
En Linux, el valor de REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT se configura en el recurso del grupo de disponibilidad del clúster. En Windows, se establece a través de Transact-SQL.

Un valor que sea mayor que 0 garantiza mayor protección de datos, porque si no está disponible el número necesario de réplicas secundarias, el servidor principal no estará disponible hasta que se resuelva. REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT afecta también al comportamiento de la conmutación por error, dado que la conmutación automática por error no podría realizarse si el número adecuado de réplicas secundarias no se encontrase en el estado correcto. En Linux, un valor de 0 no permitirá la conmutación automática por error; por tanto, en Linux, al usar la opción sincrónica con la conmutación automática por error, el valor debe ser mayor que 0 para que esta se realice. 0 en Windows Server es el comportamiento de SQL Server 2016 y de versiones anteriores.

##### <a name="enhanced-microsoft-distributed-transaction-coordinator-support"></a>Compatibilidad mejorada con Microsoft DTC (Coordinador de transacciones distribuidas)

Antes de SQL Server 2016, la única manera de obtener disponibilidad en SQL Server para las aplicaciones que requieren transacciones distribuidas que usan DTC interiormente era implementar FCI. Una transacción distribuida puede hacerse de dos maneras:
* Una transacción que abarca más de una base de datos en la misma instancia de SQL Server
* Una transacción que abarca más de una instancia de SQL Server o posiblemente implica un origen de datos diferente de SQL Server

SQL Server 2016 introdujo la compatibilidad parcial para DTC con los grupos de disponibilidad incluidos en el segundo escenario. SQL Server 2017 lo completa al hacer que ambos escenarios sean compatibles con DTC.

Otra mejora de la compatibilidad con DTC para grupos de disponibilidad es que, en SQL Server 2016, la habilitación de la compatibilidad para DTC en un grupo de disponibilidad solo se podía activar en el momento de creación del grupo de disponibilidad, y no se podía agregar en un momento posterior. En SQL Server 2017, la compatibilidad con DTC también puede agregarse a un grupo de disponibilidad después de crearlo.

>[!NOTE]
> La compatibilidad con DTC solo puede configurarse para bases de datos en instancias de SQL Server basadas en Windows Server. Si DTC es un requisito para la aplicación, debe usar Windows Server como sistema operativo para la implementación de SQL Server, y no puede usar Linux. 

#### <a name="always-on-failover-cluster-instances"></a>Instancias de clúster de conmutación por error de AlwaysOn
Las instalaciones en clúster han sido una característica de SQL Server desde la versión 6.5. Las FCI han resultado ser un método de eficacia probada a la hora de proporcionar disponibilidad para toda la instalación de SQL Server, lo que se conoce como una instancia. Esto significa que todos los elementos de la instancia, incluidas las bases de datos, los trabajos del Agente SQL Server, los servidores vinculados, etc., se moverán a otro servidor en caso que el servidor subyacente encuentre un problema. Todas las FCI requieren algún tipo de almacenamiento compartido, incluso si se proporciona a través de redes. Los recursos de la FCI solo pueden estar en ejecución y ser propiedad de un solo nodo en un momento dado. En la figura siguiente, el primer nodo del clúster posee la FCI, lo que también significa que posee los recursos de almacenamiento compartido asociados, que se indican mediante la línea continua hacia el almacenamiento.

![Instancia de clúster de conmutación por error](media/sql-server-ha-story/image3.png)
 
Después de una conmutación por error, la propiedad cambia tal y como se muestra en la figura siguiente.

![Después de conmutación por error](media/sql-server-ha-story/image4.png)
 
Con una FCI no hay pérdida de datos, pero el almacenamiento compartido subyacente es un único punto de error porque hay una copia de los datos. Las FCI se combinan a menudo con otro método de disponibilidad, como un grupo de disponibilidad o el trasvase de registros, a fin de tener copias redundantes de las bases de datos. El método adicional implementado debe usar almacenamiento físicamente separado de la FCI. Cuando la FCI conmuta por error en otro nodo, se detiene en un nodo y se inicia en otro, en un proceso no muy diferente de apagar un servidor y encenderlo. Una FCI pasa por el proceso de recuperación normal, lo que significa que las transacciones que tengan que ponerse al día se pondrán al día, y las transacciones que estén incompletas se revertirán. Por lo tanto, la base de datos es coherente desde un punto de datos hasta el momento del error o la conmutación por error manual; por lo tanto, no hay pérdida de datos. Las bases de datos solo están disponibles una vez completada la recuperación, por lo que el tiempo de recuperación dependerá de muchos factores y, en general, será más largo que la conmutación por error en un grupo de disponibilidad. La contrapartida es que cuando conmuta por error un grupo de disponibilidad, puede que sea necesario ocuparse de tareas adicionales para permitir que una base de datos se pueda utilizar, como la habilitación de un trabajo del Agente SQL Server.

Al igual que un grupo de disponibilidad, las FCI abstraen cuál es el nodo del clúster subyacente que las está hospedando. Una FCI siempre conserva el mismo nombre. Las aplicaciones y los usuarios finales nunca se conectan a los nodos; se utiliza el nombre único asignado a la FCI. Una FCI puede participar en un grupo de disponibilidad como una de las instancias que hospeda una réplica principal o secundaria.

La lista siguiente resalta algunas diferencias con las FCI en Windows Server y Linux:

* En Windows Server, una FCI es parte del proceso de instalación. Una FCI en Linux se configura después de instalar SQL Server.
* Linux solo admite una única instalación de SQL Server por host, por lo que todas las FCI serán una instancia predeterminada. Windows Server admite hasta 25 FCI por WSFC.
* El nombre común usado por las FCI en Linux se define en DNS, y debe ser el mismo que el recurso creado para la FCI.

#### <a name="log-shipping"></a>Trasvase de registros
Si el punto de recuperación y los objetivos de tiempo de recuperación son más flexibles, o las bases de datos no se consideran muy críticas, el trasvase de registros es otra característica de eficacia probada en cuanto a disponibilidad en SQL Server. En función de las copias de seguridad nativas de SQL Server, el proceso para el trasvase de registros genera de forma automática copias de seguridad del registro de transacciones, las copia en una o varias instancias conocidas como estado de espera semiactiva y aplica automáticamente las copias de seguridad del registro de transacciones a dicho estado de espera. El trasvase de registros usa trabajos del Agente SQL Server para automatizar el proceso de copia de seguridad, copia y aplicación de las copias de seguridad del registro de transacciones. 
> [!IMPORTANT] 
> En Linux, los trabajos del Agente SQL Server no se incluyen como parte de la instalación del propio SQL Server. Está disponible en los trabajos mssql-server-Agent del paquete, que también debe instalarse para usar el trasvase de registros.

![Trasvase de registros](media/sql-server-ha-story/image5.png)
 
Podría decirse que la mayor ventaja de utilizar el trasvase de registros en cierta manera es que tiene en cuenta el error humano. Es posible retrasar la aplicación de los registros de transacciones. Por lo tanto, si un usuario emite algo parecido a UPDATE sin una cláusula WHERE, el modo de espera podría no tener el cambio, así que podría cambiar a ese modo mientras repara el sistema principal. Aunque el trasvase de registros es fácil de configurar, el cambio desde el servidor principal al estado de espera semiactiva, proceso conocido como cambio de rol, siempre es manual. Un cambio de rol se inicia a través de Transact-SQL y, al igual que un grupo de disponibilidad,todos los objetos no capturados en el registro de transacciones se deben sincronizar manualmente. El trasvase de registros también debe configurarse para cada base de datos, mientras que un solo grupo de disponibilidad puede contener varias bases de datos. A diferencia de un grupo de disponibilidad o FCI, el trasvase de registros no tiene ninguna abstracción para un cambio de rol. Las aplicaciones deben ser capaces de controlar esto. Se podrían emplear técnicas como un alias de DNS (CNAME), pero esto tiene ventajas y desventajas, como el tiempo necesario para que DNS se actualice después del cambio.

## <a name="disaster-recovery"></a>Recuperación ante desastres

Cuando la ubicación de disponibilidad principal experimenta un evento catastrófico, como un terremoto o una inundación, la empresa debe estar preparada para que sus sistemas se pongan a funcionar en cualquier otro lugar. En esta sección se explica cómo pueden ser de utilidad las características de disponibilidad de SQL Server para la continuidad empresarial.

### <a name="always-on-availability-groups"></a>Grupos de disponibilidad AlwaysOn

Una de las ventajas de los grupos de disponibilidad es que tanto la alta disponibilidad como la recuperación ante desastres pueden configurarse con una sola característica. Sin necesidad de garantizar que el almacenamiento compartido tenga también una alta disponibilidad, es mucho más fácil tener réplicas que sean locales en un centro de datos para la alta disponibilidad y remotas en otros centros de datos para la recuperación ante desastres, cada una con almacenamiento independiente. El hecho de tener copias adicionales de la base de datos es la compensación para asegurar la redundancia. A continuación se muestra un ejemplo de un grupo de disponibilidad que abarca varios centros de datos. Una réplica principal es responsable de mantener todas las réplicas secundarias sincronizadas.

![Grupo de disponibilidad](media/sql-server-ha-story/image6.png)
 
Fuera de un grupo de disponibilidad con un tipo de clúster Ninguno, un grupo de disponibilidad requiere que todas las réplicas formen parte del mismo clúster subyacente, ya sea WSFC o Pacemaker. Esto significa que, en la figura anterior, el clúster WSFC se ajusta para funcionar en dos centros de datos diferentes, lo cual agrega complejidad independientemente de la plataforma (Windows Server o Linux). El ajuste de clústeres a distancia aumenta la complejidad. Introducido en SQL Server 2016, un grupo de disponibilidad distribuido permite que un grupo de disponibilidad abarque grupos de disponibilidad configurados en clústeres diferentes. Esto elimina la necesidad de que todos los nodos participen en el mismo clúster, lo que facilita en gran medida la configuración de la recuperación ante desastres. Para obtener más información sobre los grupos de disponibilidad distribuidos, consulte [Grupos de disponibilidad distribuidos](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/distributed-availability-groups).

![Grupo de disponibilidad distribuido](media/sql-server-ha-story/image11.png)
 
### <a name="always-on-failover-cluster-instances"></a>Instancias de clúster de conmutación por error de AlwaysOn

FCI puede usarse para la recuperación ante desastres. Al igual que con un grupo de disponibilidad normal, el mecanismo de clúster subyacente también se debe extender a todas las ubicaciones, lo cual incrementa complejidad. Hay algo más que se debe tener en cuenta para FCI: el almacenamiento compartido. Los mismos discos deben estar disponibles tanto en el sitio principal como en el secundario, por lo que se requiere un método externo, como la funcionalidad proporcionada por el proveedor de almacenamiento a nivel de hardware o el uso de una réplica de almacenamiento en Windows Server, para asegurarse de que los discos usados por la FCI existen en otra parte. 

![FCI de AlwaysOn](media/sql-server-ha-story/image8.png)
 
### <a name="log-shipping"></a>Trasvase de registros
El trasvase de registros es uno de los métodos más antiguo de proporcionar recuperación ante desastres para bases de datos de SQL Server. El trasvase de registros se suele usarse junto con los grupos de disponibilidad y FCI para proporcionar una funcionalidad de recuperación ante desastres más sencilla y rentable en comparación con otras opciones que pueden resultar complejas debido al entorno, las exigencias de tipo administrativo o el presupuesto. De forma similar al caso de alta disponibilidad para el trasvase de registros, muchos entornos retrasarán la carga de un registro de transacciones para tener en cuenta los errores humanos.

## <a name = "Migrations"></a> Migraciones y actualizaciones

Al implementar nuevas instancias o actualizar las antiguas, una empresa no puede asumir una interrupción prolongada. En esta sección se analizará cómo se pueden utilizar las características de disponibilidad de SQL Server para minimizar el tiempo de inactividad en un cambio de arquitectura planeado, el paso de un servidor a otro o el cambio de plataforma (por ejemplo, de Windows Server a Linux o viceversa), o durante la aplicación de revisiones.

> [!NOTE]
> Hay otros métodos, como el uso de las copias de seguridad y su restauración en otra parte, que también pueden utilizarse para las migraciones y actualizaciones. Sin embargo, no se describen en este documento. 

### <a name="always-on-availability-groups"></a>Grupos de disponibilidad AlwaysOn

Una instancia existente que contenga uno o varios grupos de disponibilidad puede actualizarse in situ a SQL Server 2017. Aunque esto requerirá cierta cantidad de tiempo de inactividad, es posible minimizarlo con una planeación correcta. 

Si el objetivo es migrar a nuevos servidores y no cambiar la configuración (incluido el sistema operativo o la versión de SQL Server), esos servidores podrían agregarse como nodos al clúster subyacente existente y, de este modo, formarán parte del grupo de disponibilidad. Una vez que la réplica o las réplicas estén en el estado correcto, podría producirse una conmutación por error manual en un servidor nuevo de modo que las antiguas se quitarían del grupo de disponibilidad y, en última instancia, se retirarían. 

Los grupos de disponibilidad distribuidos son también otro método para migrar a una configuración nueva o actualizar SQL Server. Dado que un grupo de disponibilidad distribuido admite diferentes grupos de disponibilidad en distintas arquitecturas, puede cambiar, por ejemplo, de una instancia de SQL Server 2016 que se ejecuta en Windows Server 2012 R2 a otra instancia de SQL Server 2017 que se ejecuta en Windows Server 2016. 

![Grupo de disponibilidad distribuido](media/sql-server-ha-story/image10.png)

Por último, los grupos de disponibilidad con un tipo de clúster Ninguno también pueden utilizarse para la migración o la actualización. No es posible mezclar y combinar tipos de clúster en una configuración de grupo de disponibilidad típica, por lo que todas las réplicas tendrían que ser de tipo Ninguno. Un grupo de disponibilidad distribuido puede utilizarse para abarcar grupos de disponibilidad configurados con tipos de clúster distintos. Este método también se admite en todas las plataformas de sistema operativo diferentes.

Todas las variantes de los grupos de disponibilidad para las migraciones y las actualizaciones permiten que la parte más lenta del trabajo se realice a lo largo del tiempo (sincronización de datos). Cuando llegue el momento de iniciar el cambio a la nueva configuración, el corte será una breve interrupción y no un largo período de tiempo de inactividad en el que todo el trabajo, incluida la sincronización de datos, tenga que completarse. 

Los grupos de disponibilidad pueden proporcionar un tiempo de inactividad mínimo durante la aplicación de revisiones del sistema operativo subyacente mediante la conmutación por error manual de la réplica principal a una réplica secundaria en tanto dure la aplicación de revisiones. Desde la perspectiva del sistema operativo, sera más habitual hacer esto en Windows Server puesto que a menudo, pero no siempre, el mantenimiento del sistema operativo subyacente puede requerir un reinicio. Con la aplicación de revisiones en Linux a veces es necesario reiniciar, pero es algo poco frecuente. 

[La aplicación de revisiones a instancias de SQL Server que participan en un grupo de disponibilidad](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances) también puede minimizar el tiempo de inactividad, dependiendo de la complejidad de la arquitectura del grupo de disponibilidad. A la hora de aplicar revisiones a los servidores que participan en un grupo de disponibilidad, se aplican las revisiones en primer lugar a la réplica secundaria. Una vez que se han aplicado las revisiones al número adecuado de réplicas, la réplica principal conmuta por error manualmente a otro nodo para llevar a cabo la actualización. Toda réplica secundaria restante en ese momento se puede actualizar también. 

### <a name="always-on-failover-cluster-instances"></a>Instancias de clúster de conmutación por error de AlwaysOn

La característica FCI no puede servirle de ayuda por sí misma en una migración o actualización tradicional; es necesario haber configurado un grupo de disponibilidad o un trasvase de registros para las bases de datos de la FCI y todos los demás objetos implicados. Sin embargo, las FCI en Windows Server siguen siendo una opción popular para aquellos casos en que es necesario aplicar una revisión a los servidores de Windows Server subyacentes. Puede iniciar una conmutación por error manual, lo que implica una breve interrupción en lugar de tener la instancia completamente no disponible durante todo el tiempo en que se están aplicando las revisiones a Windows Server.
Una FCI se puede actualizar in situ a SQL Server 2017. Para obtener más información, consulte [Actualizar una instancia de clúster de conmutación por error de SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance).

### <a name="log-shipping"></a>Trasvase de registros

El trasvase de registros sigue siendo una opción popular para migrar y actualizar bases de datos. De forma similar a los grupos de disponibilidad, pero esta vez utilizando el registro de transacciones como método de sincronización, la propagación de datos se puede iniciar antes del cambio de servidor. En el momento del cambio, una vez que se detiene todo el tráfico en el origen, será necesario tomar, copiar y aplicar un registro de transacciones final a la nueva configuración. En ese momento, la base de datos se puede poner en línea. El trasvase de registros suele ser más tolerante con las redes más lentas, y mientras que la conmutación puede ser ligeramente más larga que otra que se realice mediante un grupo de disponibilidad o un grupo de disponibilidad distribuido, normalmente se mide en minutos (no horas, días ni semanas).

Al igual que los grupos de disponibilidad, el trasvase de registros puede proporcionar un mecanismo que permite cambiar a otro servidor en caso de aplicación de revisiones.

### <a name="other-sql-server-deployment-methods-and-availability"></a>Otros métodos de implementación de SQL Server y disponibilidad

Hay otros dos métodos de implementación para SQL Server en Linux: contenedores y uso de Azure (u otro proveedor de nube pública). La necesidad generalizada de disponibilidad, tal como se presenta en este documento, existe con independencia de cómo se implemente SQL Server. Estos dos métodos tienen algunas consideraciones especiales en lo relativo a hacer que SQL Server tenga alta disponibilidad.

Los [contenedores con Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker) son una nueva manera de implementar SQL Server, ya sea para Windows Server o para Linux. Un contenedor es una imagen completa de SQL Server que está lista para ejecutarse. Sin embargo, actualmente no existe compatibilidad nativa para la agrupación en clústeres, y por lo tanto, para la alta disponibilidad directa o la recuperación ante desastres. Actualmente, las opciones para hacer que las bases de datos de SQL Server estén disponibles mediante el uso de contenedores serían el trasvase de registros y la copia de seguridad y restauración. Si bien es posible configurar un grupo de disponibilidad con un tipo de clúster Ninguno, como se indicó anteriormente, esta no se considera una auténtica configuración de disponibilidad. Microsoft está examinando la manera de habilitar los grupos de disponibilidad o las FCI con contenedores. 

Si está utilizando contenedores en la actualidad, en caso de que el contenedor se pierda, es posible implementarlo de nuevo y adjuntarlo al almacenamiento compartido que se utilizó (dependiendo de la plataforma del contenedor). Parte de este mecanismo lo ofrece el organizador de contenedores. Aunque esto proporciona cierta resiliencia, habrá un determinado tiempo de inactividad asociado con la recuperación de la base de datos, y no tendría realmente la misma alta disponibilidad que si se utilizara un grupo de disponibilidad o una FCI. 

Es posible implementar máquinas virtuales IaaS de Linux con SQL Server instalado utilizando Azure. Al igual que en las instalaciones basadas en un sistema local, una instalación compatible requiere el uso de STONITH (Shoot the Other Node in the Head), que es externo al propio Pacemaker. STONITH se proporciona a través de agentes de disponibilidad que actúan como barrera. Algunas distribuciones los incluyen como parte de la plataforma, otras dependen de los proveedores externos de hardware y software. Póngase en contacto con su distribuidor de Linux preferido para ver de qué manera se proporciona STONITH de modo que pueda implementar una solución admitida en la nube pública.

## <a name="cross-platform-and-linux-distribution-interoperability"></a>Interoperabilidad de distribución multiplataforma y Linux

Ahora que SQL Server se admite en Windows Server y Linux, en esta sección se tratan los escenarios en que ambas plataformas pueden funcionar en conjunto para ofrecer disponibilidad, además de para otros fines, así como el caso de las soluciones que incorporan más de una distribución de Linux.

Antes de tratar los escenarios de interoperabilidad y multiplataforma, es necesario poner dos hechos de relieve:

* En ninguna situación una FCI o un grupo de disponibilidad basado en WSCF funcionará directamente con una FCI o un grupo de disponibilidad basado en Linux. Un WSCF no se puede extender por un nodo de Pacemaker, y viceversa. 
* No se admite la combinación de las distribuciones de Linux con FCI o un grupo de disponibilidad que tenga un clúster de tipo Externo. Todas las réplicas de los grupos de disponibilidad en ese escenario deben estar configurados no solo con la misma distribución de Linux, sino también con la misma versión. Las dos formas admitidas de que SQL Server pueda funcionar en las dos plataformas o varias distribuciones de Linux son los grupos de disponibilidad y el trasvase de registros.

## <a name="distributed-availability-groups"></a>Grupos de disponibilidad distribuidos 

Los grupos de disponibilidad distribuidos están diseñados para abarcar las configuraciones de grupo de disponibilidad, con independencia de que los dos clústeres subyacentes debajo de los grupos de disponibilidad sean dos clústeres WSFC diferentes, distribuciones de Linux, o uno esté en un clúster WSFC y otro en Linux. Un grupo de disponibilidad distribuido será el método principal de contar con una solución multiplataforma. Un grupo de disponibilidad distribuido es también la solución principal para las migraciones del tipo de una conversión desde una infraestructura de SQL Server basada en Windows Server a otra basada en Linux, en caso de que sea esto lo que quiere hacer su empresa. Como se mencionó anteriormente, los grupos de disponibilidad, y especialmente los grupos de disponibilidad distribuidos, minimizarán el tiempo durante el que una aplicación podría estar no disponible para su uso. A continuación se muestra un ejemplo de un grupo de disponibilidad distribuido que abarca un clúster WSFC y Pacemaker.

![Grupo de disponibilidad distribuido](media/sql-server-ha-story/image9.png)
 
Si se configura un grupo de disponibilidad con un clúster de tipo Ninguno, este puede abarcar Windows Server y Linux, así como varias distribuciones de Linux. Puesto que esta no es una auténtica configuración de alta disponibilidad, no debe utilizarse para las implementaciones críticas, sino para escenarios de escala de lectura o de migración o actualización.

## <a name="log-shipping"></a>Trasvase de registros

Dado que el trasvase de registros se basa simplemente en la copia de seguridad y restauración, no existen diferencias en las bases de datos, las estructuras de archivos, etc., para SQL Server en Windows Server en comparación con SQL Server en Linux. Esto significa que se puede configurar el trasvase de registros entre una instalación de SQL Server basada en Windows Server y otra de Linux, así como entre distintas distribuciones de Linux. Todo lo demás permanece igual. La única advertencia es que el trasvase de registros, al igual que un grupo de disponibilidad, no puede funcionar cuando el origen se encuentra en una versión principal de SQL Server posterior en relación con un destino que está en una versión anterior de SQL Server. 

## <a name = "ReadScaleOut"></a> Escalado de lectura

Desde su introducción en SQL Server 2012, las réplicas secundarias han podido utilizarse para consultas de solo lectura. Hay dos maneras de hacerlo con un grupo de disponibilidad: permitiendo el acceso directo a la secundaria, así como [configurando el enrutamiento de solo lectura](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server), lo que requiere el uso del agente de escucha.  SQL Server 2016 introdujo la posibilidad de equilibrar la carga de las conexiones de solo lectura a través del agente de escucha mediante un algoritmo round-robin, lo que permite a las solicitudes de solo lectura su expansión por todas las réplicas legibles. 

> [!NOTE]
> Las réplicas secundarias legibles son una característica exclusiva de Enterprise Edition, y cada instancia que hospeda una réplica legible necesitará una licencia de SQL Server.

El escalado de copias legibles de una base de datos a través de grupos de disponibilidad apareció por primera vez con los grupos de disponibilidad distribuidos en SQL Server 2016. Esto permitió a las empresas contar con copias de solo lectura de la base de datos no solo localmente, sino también a nivel regional y mundial con una cantidad mínima de configuración, y reducir el tráfico de red y la latencia gracias a que las consultas se ejecutan localmente. Cada réplica principal de un grupo de disponibilidad puede inicializar dos otros grupos de disponibilidad, incluso si no es la copia de lectura/escritura completa, por lo que cada grupo de disponibilidad distribuido puede admitir hasta 27 copias de los datos que son legibles. 

![Grupo de disponibilidad distribuido](media/sql-server-ha-story/image11.png)

A partir de SQL Server 2017, es posible crear una solución de solo lectura casi en tiempo real con la configuración de grupos de disponibilidad con un clúster de tipo Ninguno. Si el objetivo radica en utilizar grupos de disponibilidad para las réplicas secundarias legibles y no en la disponibilidad, esta opción elimina la complejidad de utilizar un clúster WSFC o Pacemaker, y ofrece las ventajas legibles de un grupo de disponibilidad en un método de implementación más sencillo. 

La única advertencia importante es que como no hay ningún clúster subyacente con un clúster de tipo Ninguno, la configuración del enrutamiento de solo lectura es un poco diferente. Desde una perspectiva de SQL Server, un agente de escucha sigue siendo necesario para enrutar las solicitudes, incluso si no hay ningún clúster. En lugar de configurar un agente de escucha tradicional, se utiliza la dirección IP o el nombre de la réplica principal. La réplica principal se usa entonces para enrutar las solicitudes de solo lectura.

Técnicamente, se puede configurar un estado de espera semiactiva de trasvase de registros para el uso legible mediante la restauración de la base de datos WITH STANDBY. Sin embargo, dado que los registros de transacciones requieren el uso exclusivo de la base de datos para la restauración, los usuarios no podrán acceder a la base de datos mientras esto ocurre. Por ello, el trasvase de registros es una solución menos idónea, especialmente si se necesitan datos casi en tiempo real. 

Un aspecto que debe tenerse en cuenta para todos los escenarios de escalado de lectura con grupos de disponibilidad es que, a diferencia de la replicación transaccional donde todos los datos están activos, cada réplica secundaria no está en un estado en el que se puedan aplicar los índices únicos: la réplica es una copia exacta de la principal. Esto significa que, en caso de que se requieran índices para la creación de informes o sea necesario manipular datos, debe hacerse en las bases de datos de la réplica principal. Si necesita esa flexibilidad, la replicación es una mejor solución para datos legibles.

## <a name="summary"></a>Resumen

Las instancias y las bases de datos de SQL Server 2017 pueden hacerse de alta disponibilidad usando las mismas características en Windows Server y Linux. Además de los escenarios de disponibilidad estándar de alta disponibilidad y recuperación ante desastres local, se puede minimizar el tiempo de inactividad asociado a las actualizaciones y las migraciones con las características de disponibilidad de SQL Server. Los grupos de disponibilidad también pueden proporcionar copias adicionales de una base de datos como parte de la misma arquitectura para escalar horizontalmente copias legibles. Si va a implementar una nueva solución con SQL Server 2017 o está considerando la aplicación de una actualización, SQL Server 2017 tiene la disponibilidad y confiabilidad que necesita.
 
[SimpleAG]:media\sql-server-ha-story\image1.png
[SSMSAGOptions]:media\sql-server-ha-story\image2.png
[BasicFCI]:media\sql-server-ha-story\image3.png
[PostFailoverFCI]:media\sql-server-ha-story\image4.png
[LogShipping]:media\sql-server-ha-story\image5.png
[AG]:media\sql-server-ha-story\image6.png
[DAG]:media\sql-server-ha-story\image7.png
[AlwaysOnFCI]:media\sql-server-ha-story\image8.png
[BasicDAG]:media\sql-server-ha-story\image9.png
[image10]:media\sql-server-ha-story\image10.png
[DAG]:media\sql-server-ha-story\image11.png
