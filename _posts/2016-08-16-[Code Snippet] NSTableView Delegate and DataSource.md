---
layout: post
title:  "[Code Snippet] NSTableView Delegate and DataSource"
date:   2016-08-16
desc: "[Code Snippet] NSTableView Delegate and DataSource"
keywords: "MacOS,Code Snippet"
categories: [HTML]
tags: [MacOS]
icon: icon-javascript
---

<pre><code>
#pragma mark - NSTableViewDataSource

- (NSInteger)numberOfRowsInTableView:(NSTableView *)tableView {
    return <#count#>;
}

#pragma mark - NSTableViewDelegate

- (CGFloat)tableView:(NSTableView *)tableView heightOfRow:(NSInteger)row {
    return <#height#>;
}

- (NSView *)tableView:(NSTableView *)tableView viewForTableColumn:(NSTableColumn *)tableColumn row:(NSInteger)row {

    // Get an existing cell with the MyView identifier if it exists
    NSTextField *result = [tableView makeViewWithIdentifier:@"<#view identifier#>" owner:self];

    // There is no existing cell to reuse so create a new one
    if (result == nil) {
        // Create the new NSTextField with a frame of the {0,0} with the width of the table.
        // Note that the height of the frame is not really relevant, because the row height will modify the height.
        result = [[NSTextField alloc] initWithFrame:<#frame#>];
    
        // The identifier of the NSTextField instance is set to MyView.
        // This allows the cell to be reused.
        result.identifier = @"<#view identifier#>";
    }
    
    // result is now guaranteed to be valid, either as a reused cell
    // or as a new cell, so set the stringValue of the cell to the
    // nameArray value at row
    result.stringValue = [<#object array#> objectAtIndex:row];
    
    // Return the result
    return result;
}
</code></pre>