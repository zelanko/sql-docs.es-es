---
title: Ejemplo de flujo de trabajo personalizado (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 010b733826f55bed55a246297bd9b5aa08b9aadc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62519299"
---
# <a name="create-a-custom-workflow---example"></a>Crear un flujo de trabajo personalizado: Ejemplo

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], cuando crea una biblioteca de clases de flujo de trabajo personalizado, crea una clase que implementa la interfaz Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender. Esta interfaz incluye un método, <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>, al que el servicio de integración de flujos de trabajo MDS de SQL Server llama cuando se inicia un flujo de trabajo. El método <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> contiene dos parámetros: *workflowType* contiene el texto especificado en el cuadro **Tipo de flujo de trabajo** en [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], y *dataElement* contiene datos de elementos y metadatos para el elemento que desencadenó la regla de negocio del flujo de trabajo.  
  
## <a name="custom-workflow-example"></a>Ejemplo de flujo de trabajo personalizado  
 En el ejemplo de código siguiente se muestra cómo implementar el método <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> para extraer los atributos Name, Code y LastChgUserName de los datos XML del elemento que desencadenó la regla de negocio del flujo de trabajo, y cómo llamar a un procedimiento almacenado para insertarlos en otra base de datos. Para ver un ejemplo del código XML de datos de elementos y una explicación de las etiquetas que este contiene, vea [Descripción del código XML de flujo de trabajo personalizado &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Crear un flujo de trabajo personalizado &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  
