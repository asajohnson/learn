## Create a dynamic group with all users as members

1. Sign in to the [Azure portal](https://portal.azure.com/) with an account that is assigned the Global administrator or User administrator role in the tenant.
1. Select **Azure Active Directory**.
1. Under **Manage**, select **Groups**, and then select **New group**.
1. On the New Group page, under **Group type**, select **Security**.
1. In the **Group name** box, enter **All company users dynamic group**.
1. Select the **Membership type** menu and then select **Dynamic User**.
1. Under **Dynamic user members**, select **Add dynamic query**.
1. On the right above the **Rule syntax** box, select **Edit**.
1. In the Edit rule syntax pane, enter the following expression in the **Rule syntax** box: user.objectId -ne null
1. Select **OK**. The rule appears in the Rule syntax box.
    
    :::image type="content" source="../media/dynamic-group-membership-rule-ff845a55.png" alt-text="Screenshot of the dynamic group membership rules screen with rule syntax highlighted. Exist in Azure A D.":::
    
1. Select **Save**. The new dynamic group will now include B2B guest users as well as member users.
1. On the New group page, select **Create** to create the group.
