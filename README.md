# Classforma-Frontend-Intern-Assessment
# WorkflowListPage
import React, { useEffect, useState } from 'react';
import { useHistory } from 'react-router-dom';
import Table from 'react-table';

function WorkflowListPage() {
  const history = useHistory();
  const [workflows, setWorkflows] = useState([]);

  useEffect(() => {
    async function fetchWorkflows() {
      const response = await fetch('/api/workflows');
      const data = await response.json();
      setWorkflows(data);
    }

    fetchWorkflows();
  }, []);

  const columns = [
    {
      Header: 'Name',
      accessor: 'name',
    },
    {
      Header: 'Input Type',
      accessor: 'inputType',
    },
    {
      Header: 'Created At',
      accessor: 'createdAt',
    },
  ];

  const handleCreateWorkflow = () => {
    history.push('/workflow-designer/new');
  };

  return (
    <div>
      <h1>Workflow List</h1>
      <button onClick={handleCreateWorkflow}>Create New Workflow</button>
      <Table columns={columns} data={workflows} />
    </div>
  );
}

export default WorkflowListPage;
