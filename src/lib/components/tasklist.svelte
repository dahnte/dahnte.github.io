<script>
    import * as Table from "$lib/components/ui/table/index.js";
    import { Badge } from "$lib/components/ui/badge/index.js";
</script>

<Table.Root>
    <Table.Caption>Get these done today!</Table.Caption>
    <Table.Header>
        <Table.Row>
            <Table.Head class="w-[65%]">Task</Table.Head>
            <Table.Head class="text-right">Status</Table.Head>
        </Table.Row>
    </Table.Header>
    <Table.Body>
        <Table.Row>
            <Table.Cell class="font-medium">Demo dashboard</Table.Cell>
            <Table.Cell class="text-right">
                <Badge variant="outline">In Progress</Badge>
            </Table.Cell>
        </Table.Row>
        <Table.Row>
            <Table.Cell class="font-medium">Build Your Own Schedule</Table.Cell>
            <Table.Cell class="text-right">
                <Badge>Complete</Badge>
            </Table.Cell>
        </Table.Row>
        <Table.Row>
            <Table.Cell class="font-medium">Finish demo dashboard</Table.Cell>
            <Table.Cell class="text-right">
                <Badge variant="outline">In Progress</Badge>
            </Table.Cell>
        </Table.Row>
        <Table.Row>
            <Table.Cell class="font-medium">Finish demo dashboard</Table.Cell>
            <Table.Cell class="text-right">
                <Badge variant="outline">In Progress</Badge>
            </Table.Cell>
        </Table.Row>
        <Table.Row>
            <Table.Cell class="font-medium">Finish demo dashboard</Table.Cell>
            <Table.Cell class="text-right">
                <Badge variant="outline">In Progress</Badge>
            </Table.Cell>
        </Table.Row>
        <Table.Row>
            <Table.Cell class="font-medium">Finish demo dashboard</Table.Cell>
            <Table.Cell class="text-right">
                <Badge variant="outline">In Progress</Badge>
            </Table.Cell>
        </Table.Row>
        <Table.Row>
            <Table.Cell class="font-medium">Finish demo dashboard</Table.Cell>
            <Table.Cell class="text-right">
                <Badge variant="outline">In Progress</Badge>
            </Table.Cell>
        </Table.Row>
    </Table.Body>
</Table.Root>