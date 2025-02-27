## 内部账户管理流程图

以下是《鞍山银行内部账户管理办法（2024版）》中内部账户开立、变更和销户的流程图，使用 Mermaid 语法编写。

```mermaid
graph TD;
    %% 流程起点
    Start((开始)) --> Decision[申请发起单位];
    
    %% 决策点：申请发起单位
    Decision -->|总行本级业务部门| TotalBankApply[业务部门填写申请表];
    Decision -->|分支行业务部门| BranchApply[业务部门填写申请表];
    
    %% 总行本级业务部门路径
    subgraph 总行本级业务部门申请流程
        TotalBankApply --> TotalBankSubmit[提交至运营管理部审核];
        TotalBankSubmit --> TotalBankCheck{运营管理部审核};
        TotalBankCheck -->|通过| TotalBankApprove[提交至计划财务部审批];
        TotalBankCheck -->|不通过| TotalBankModify[返回业务部门修改];
        TotalBankModify --> TotalBankApply;
        TotalBankApprove --> TotalBankFinalCheck{计划财务部审批};
        TotalBankFinalCheck -->|通过| TotalBankExecute[运营管理部执行操作];
        TotalBankFinalCheck -->|不通过| TotalBankEnd[流程终止];
        TotalBankExecute --> TotalBankReport[业务部门报备计划财务部];
        TotalBankReport --> End;
    end
    
    %% 分支行业务部门路径
    subgraph 分支行业务部门申请流程
        BranchApply --> BranchSubmit[提交至总行本级业务归口部门审核];
        BranchSubmit --> BranchCheck{归口部门审核};
        BranchCheck -->|通过| BranchOpsCheck[提交至运营管理部审核];
        BranchCheck -->|不通过| BranchModify[返回分支行修改];
        BranchModify --> BranchApply;
        BranchOpsCheck --> BranchOpsDecision{运营管理部审核};
        BranchOpsDecision -->|通过| BranchApprove[提交至计划财务部审批];
        BranchOpsDecision -->|不通过| BranchOpsModify[返回分支行修改];
        BranchOpsModify --> BranchApply;
        BranchApprove --> BranchFinalCheck{计划财务部审批};
        BranchFinalCheck -->|通过| BranchExecute[运营管理部执行操作];
        BranchFinalCheck -->|不通过| BranchEnd[流程终止];
        BranchExecute --> BranchReport[分支行报备计划财务部];
        BranchReport --> End;
    end
    
    %% 流程终点
    End((结束))
