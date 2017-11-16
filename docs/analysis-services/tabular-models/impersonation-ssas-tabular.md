---
title: "Suplantación en los modelos tabulares de Analysis Services | Documentos de Microsoft"
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 6d18cbe5b20882581afa731ce5d207cbbc69be6c
ms.openlocfilehash: aef09b5327408701f15e484bbcea1cab9d82622b
ms.contentlocale: es-es
ms.lasthandoff: 10/21/2017

---
# <a name="impersonation"></a>Suplantación 

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Este tema proporciona a los autores de modelos tabulares una descripción de cómo las credenciales de inicio de sesión se usa Analysis Services cuando se conecta a un origen de datos para importar y procesar (actualizar) los datos.  

##  <a name="bkmk_conf_imp_info"></a>Configurar la suplantación  
 El lugar y en qué contexto existe un modelo determina cómo se configura la información de suplantación. Al crear un nuevo proyecto de modelo, la suplantación se configura en SQL Server Data Tools (SSDT) cuando se conecta a un origen de datos para importar datos. Una vez implementado un modelo, suplantación puede configurarse en la propiedad de cadena de conexión de base de datos de modelo mediante el uso de SQL Server Management Studio (SSMS). Para los modelos tabulares en Analysis Services de Azure, puede usar SSMS o **ver como: Script** modo en el diseñador basado en navegador para editar el archivo Model.bim en JSON.
  
##  <a name="bkmk_how_imper"></a>¿Cómo se utiliza la suplantación  
 La*suplantación* es la capacidad de una aplicación de servidor, como Analysis Services, de asumir la identidad de una aplicación cliente. Analysis Services se ejecuta con una cuenta de servicio; sin embargo, cuando el servidor establece una conexión a un origen de datos, utiliza la suplantación para que las comprobaciones de acceso para la importación de datos y el procesamiento se puede realizar.  
  
 Son diferentes de las credenciales que han iniciado sesión con las credenciales usadas para la suplantación. Usuario que inició sesión credenciales se utilizan para las operaciones de cliente determinadas al crear un modelo.  
  
 Es importante entender cómo se especifica y protegidas, así como la diferencia entre los contextos en los que tanto la que inició sesión en las credenciales de suplantación se usan las credenciales de usuario y cuando se usan otras credenciales de suplantación.  
  
 **Descripción de las credenciales de servidor**  
 
Cuando se importan o procesan datos, las credenciales de suplantación se usan para conectarse al origen de datos y capturar los datos. Se trata de un *servidor* operación que se ejecute en el contexto de una aplicación cliente porque el servidor de Analysis Services que hospeda la base de datos del área de trabajo se conecta al origen de datos y captura los datos.  
  
 Al implementar un modelo en un servidor de Analysis Services, si la base de datos del área de trabajo está en la memoria cuando se implementa el modelo, las credenciales se pasan al servidor de Analysis Services en el que se implementa el modelo. Las credenciales de usuario no se almacenan en el disco en ningún momento.  
  
 Cuando un modelo implementado procesa los datos de un origen de datos, las credenciales de suplantación, almacenadas en la base de datos en memoria, se utilizan para conectarse al origen de datos y capturar los datos. Dado que este proceso lo controla el servidor de Analysis Services que administra la base de datos de modelo, esta también es una operación de servidor.  
  
 **Descripción de las credenciales de cliente**  
  
 Al crear un nuevo modelo o al agregar un origen de datos a un modelo existente, conectarse a un origen de datos y seleccionar tablas y vistas que se importarán en el modelo. En el Asistente para importación de tablas o el Diseñador de Data\Query obtener vista previa y filtrar de características, verá un ejemplo de los datos que se importan. También puede especificar filtros para excluir los datos que no es necesario incluir en el modelo.  
  
 De forma similar, para los modelos que ya se ha creado, use el **propiedades de la tabla** cuadro de diálogo Vista previa y filtrar datos importados en una tabla.  
  
 Las características de vista previa y filtro, **propiedades de la tabla**, y **Partition Manager** cuadros de diálogo están en proceso *cliente* operación; es decir, lo que se realiza durante la ejecución operación es diferente de cómo se conecta el origen de datos a y se capturan datos desde el origen de datos; una operación de servidor. Las credenciales utilizadas para obtener una vista previa y filtrar los datos son las credenciales del usuario que ha iniciado sesión actualmente. En efecto, sus credenciales. 
  
 La separación de las credenciales que se usa durante del servidor y las operaciones del lado cliente pueden dar lugar a un error de coincidencia en lo que se ve y qué datos se capturan durante una importación o un proceso (una operación de servidor). Si las credenciales se ha iniciado sesión actualmente con y las credenciales de suplantación especificadas son diferentes, los datos se ven en las características de vista previa y filtrar o **propiedades de la tabla** cuadro de diálogo y los datos capturados durante una importación o proceso puede ser diferente, dependiendo de las credenciales requeridas por el origen de datos.  
  
> [!IMPORTANT]  
>  Al crear un modelo, asegúrese de que las credenciales que ha iniciado sesión con y las credenciales especificadas para la suplantación tienen derechos suficientes para capturar los datos del origen de datos.  
  
##  <a name="bkmk_imp_info_options"></a> Opciones  
 Al configurar la suplantación, o al modificar las propiedades de una conexión de origen de datos existente, especifique una de las siguientes opciones:  
  
**Modelos tabulares 1400 y versiones posteriores**
 
|Opción|Description|  
|------------|-----------------|  
|**Suplantar la cuenta**|Especifica el modelo usa una cuenta de usuario de Windows para importar o procesar datos desde el origen de datos. El dominio y el nombre de la cuenta de usuario tienen el siguiente formato:**\<nombre de dominio >\\< nombre de la cuenta de usuario\>**.|  
|**Suplantar al usuario actual**|Especifica que deben tener acceso a datos desde el origen de datos utilizando la identidad del usuario que envió la solicitud. Este modo se aplica solo a modo de consulta directa.|  
|**Suplantar la identidad**|Especifica un nombre de usuario para tener acceso a origen de datos, pero no es necesario especificar la contraseña de la cuenta. Este modo se aplica solo cuando la delegación Kerberos está habilitada y especifica que se debe usar la autenticación de S4U.|  
|**Suplantar la cuenta de servicio**|Especifica el modelo usa las credenciales de seguridad asociadas a la instancia de servicio de Analysis Services que administra el modelo.|  
|**Suplantar la cuenta desatendida**|Especifica que el motor de Analysis Services debe usar una cuenta desatendida preconfigurada para tener acceso a los datos.|  


**Modelos tabulares 1200**
 
|Opción|Description|  
|------------|-----------------|  
|**Contraseña y nombre de usuario de Windows específico**|Esta opción especifica el modelo usa una cuenta de usuario de Windows para importar o procesar datos desde el origen de datos. El dominio y el nombre de la cuenta de usuario tienen el siguiente formato:**\<nombre de dominio >\\< nombre de la cuenta de usuario\>**. Esta es la opción predeterminada al crear un modelo nuevo mediante el Asistente para la importación de tablas.|  
|**Cuenta de servicio**|Esta opción especifica que el modelo usa las credenciales de seguridad asociadas a la instancia de servicio de Analysis Services que administra el modelo.|  
  
##  <a name="bkmk_impers_sec"></a> Seguridad  
 Las credenciales utilizadas con suplantación son almacena en memoria el motor de VertiPaq™. Credenciales nunca se escriben en el disco. Si la base de datos del área de trabajo no está en memoria cuando se implementa el modelo, se pedirá al usuario que escriba las credenciales usadas para conectarse a los datos de origen de datos y fetch.  
  
> [!NOTE]  
>  Se recomienda especificar una cuenta de usuario y una contraseña de Windows para las credenciales de suplantación. Una cuenta de usuario de Windows puede configurarse para utilizar los privilegios mínimos necesarios para conectarse a y leer datos desde el origen de datos.  
  

  
## <a name="see-also"></a>Vea también  
 [Modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Orígenes de datos](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [Implementación de la solución de modelo tabular](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  

