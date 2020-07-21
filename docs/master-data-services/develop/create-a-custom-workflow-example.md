---
title: Ejemplo de flujo de trabajo personalizado
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: reference
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 880cf38105bd70198a52c55feec151e163f21c28
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900989"
---
# <a name="create-a-custom-workflow---example"></a>Crear un flujo de trabajo personalizado: Ejemplo

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], cuando crea una biblioteca de clases de flujo de trabajo personalizado, crea una clase que implementa la interfaz Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender. Esta interfaz incluye un método, [Microsoft. MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130)) , al que llama SQL Server servicio de integración de flujos de trabajo de MDS cuando se inicia un flujo de trabajo. El método [Microsoft. MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130)) contiene dos parámetros: *workflowType* contiene el texto que escribió en el cuadro de texto **tipo de flujo de trabajo** en [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , y el *elemento* DataItem contiene metadatos y datos de elementos para el elemento que desencadenó la regla de negocio del flujo de trabajo.  
  
## <a name="custom-workflow-example"></a>Ejemplo de flujo de trabajo personalizado  
 En el ejemplo de código siguiente se muestra cómo implementar el método [Microsoft. MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130)) para extraer el nombre, el código y los atributos de LastChgUserName de los datos XML para el elemento que desencadenó la regla de negocio del flujo de trabajo y cómo llamar a un procedimiento almacenado para insertarlos en otra base de datos. Para ver un ejemplo del código XML de datos de elementos y una explicación de las etiquetas que este contiene, vea [Descripción del código XML de flujo de trabajo personalizado &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md).  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.Data.SqlClient;  
using System.Xml;  
  
using Microsoft.MasterDataServices.Core.Workflow;  
  
namespace MDSWorkflowTestLib  
{  
    public class WorkflowTester : IWorkflowTypeExtender  
    {  
        #region IWorkflowTypeExtender Members  
  
        public void StartWorkflow(string workflowType, System.Xml.XmlElement dataElement)  
        {  
            // Extract the attributes we want out of the element data.  
            XmlNode NameNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Name");  
            XmlNode CodeNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Code");  
            XmlNode EnteringUserNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/LastChgUserName");  
  
            // Open a connection on the workflow database.  
            SqlConnection workflowConn = new SqlConnection(@"Data Source=<Server instance>; Initial Catalog=WorkflowTest; Integrated Security=True");  
  
            // Create a command to call the stored procedure that adds a new user to the workflow database.  
            SqlCommand addCustomerCommand = new SqlCommand("AddNewCustomer", workflowConn);  
            addCustomerCommand.CommandType = System.Data.CommandType.StoredProcedure;  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Name", NameNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Code", CodeNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@EnteringUser", EnteringUserNode.InnerText));  
  
            // Execute the command.  
            workflowConn.Open();  
            addCustomerCommand.ExecuteNonQuery();  
            workflowConn.Close();  
        }  
  
        #endregion  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Crear un flujo de trabajo personalizado &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  
