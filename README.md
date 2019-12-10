page 50110 ALIssueList
{
    PageType = List;
    SourceTable = ALIssue;
    CaptionML = ENU = 'AL Issues';
    Editable = false;
    SourceTableView = order(descending);

    layout
    {
        area(content)
        {
            repeater(General)
            {
                field(Number; number) { }
                field(Title; title) { }
                field(CreatedAt; created_at) { }
                field(User; user) { }
                field(State; state) { }
                field(URL; html_url)
                {
                    ExtendedDatatype = URL;
                }
            }
        }
    }

    actions
    {
        area(processing)
        {
            action(RefreshALIssueList)
            {
                CaptionML = ENU = 'Refresh Issues';
                Promoted = true;
                PromotedCategory = Process;
                Image = RefreshLines;
                trigger OnAction();
                var

                begin
                    RefreshIssues();
                    CurrPage.Update;
                    Message('Done');
                    if FindFirst then;
                end;
            }

        }
    }

    trigger OnOpenPage();
    begin
        RefreshIssues();
        MESSAGE('Version Contro Testing');
        Message('TEST2');
        if FindFirst then;
    end;

}