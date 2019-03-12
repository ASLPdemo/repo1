## API list:

	createNode(nodeDate_dict dict):
	SQL: "INSERT INTO dynamic(keys) VALUES (values)
	return bl:True/False

	listNodeAll():
	sqlStatement="SELECT * FROM node;"
	rs=query(sqlStatement)
	return rs

	listNode(nodeId):
	sqlStatement="SELECT * FROM node WHERE id IN (" + nodeId + ");"
	rs=query(sqlStatement)
	return rs

	createGroup(valueList):
	sqlStatement="INSERT INTO group_node_map(id,node_id,group_id) VALUES("+valueList+");"
	rs=query(sqlStatement)
	return rs

	listGroupAll():
	sqlStatement="SELECT node_id,group_id FROM group_node_map ORDER BY node_id;"
	rs=query(sqlStatement)
	rs=present_group(rs)
	return rs
listGroup(groupId):
	sqlStatement="SELECT * FROM group_node_map WHERE group_id IN(" + groupId + ");"
	rs=query(sqlStatement)
	rs=present_group(rs)
	return rs
deleteGroupRelation(groupId):
	sqlStatement = 'DELETE FROM group_node_map WHERE group_id='+str(groupId)+';'
	rs=query(sqlStatement)
	return rs
insertGroupRelation(node_id,groupId):
	sqlStatement = 'INSERT INTO group_node_map(node_id,group_id) VALUES('+str(node_id)+','+str(groupId)+');'
	rs=query(sqlStatement)
	return rs
listCaution(node_id = None,limit = 50):
	if node_id == None:
		sqlStatement="SELECT * FROM caution ORDER BY issue_date DESC limit "+str(limit)+";"
	else:
		sqlStatement="SELECT * FROM caution WHERE node_id = "+str(node_id)+" ORDER BY issue_date DESC limit "+str(limit)+";"
	rs=query(sqlStatement)
	return rs
listRunTime():
	sqlStatement="SELECT * FROM node_runtime ORDER BY node_id;"
	rs=query(sqlStatement)
	return rs
nodePower(node_id,power_bl):
	sqlStatement="UPDATE node_runtime SET POWER="+power_bl+" WHERE node_id="+node_id+";"
	rs=query(sqlStatement)
	return rs

updateDynamic(dynamicData_dict):
	(keys,values) = zip(*dynamicData_dict.items())
	keys = ','.join(str(e) for e in keys)
	sqlStatement="INSERT INTO dynamic("+keys+") VALUES"+str(values)+";"
	rs=query(sqlStatement)
	return rs
