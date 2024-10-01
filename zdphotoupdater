import requests
import os
from requests.auth import HTTPBasicAuth

# Zendesk API details
zendesk_domain = 'INSERTBRANDHERE.zendesk.com'  # e.g., 'yourcompany.zendesk.com'
email = 'EMAILHERE/token'  # Zendesk email
api_token = 'TOKEN_HERE'  # Zendesk API token

# Group filter (to match "unique_string")
group_filter = 'unique_string'

# Path to the profile picture file on your desktop
image_path = os.path.expanduser("~/Desktop/cdlogo.png")  # Update with actual image filename

# API base URL
api_url = f'https://{zendesk_domain}/api/v2'

def get_unique_string_group_ids():
	"""Fetch all groups with 'unique_string' in the name"""
	url = f'{api_url}/groups.json'
	response = requests.get(url, auth=HTTPBasicAuth(email, api_token))

	if response.status_code != 200:
		print(f"Failed to fetch groups. Status Code: {response.status_code}, Response: {response.text}")
		return []

	groups = response.json()['groups']
	print(f"Fetched Groups: {groups}")  # Print fetched groups for debugging

	unique_string_group_ids = [group['id'] for group in groups if group_filter.lower() in group['name'].lower()]
	return unique_string_group_ids

def get_users_in_groups(group_ids):
	"""Fetch all users in specified groups"""
	users = []
	for group_id in group_ids:
		url = f'{api_url}/groups/{group_id}/users.json'
		response = requests.get(url, auth=HTTPBasicAuth(email, api_token))

		if response.status_code != 200:
			print(f"Failed to fetch users for group {group_id}")
			continue

		users.extend(response.json()['users'])
	return users

def update_user_profile_picture(user_id, image_path):
	"""Update the user's profile picture"""
	with open(image_path, 'rb') as image_file:
		image_data = {'avatar': image_file}
		url = f'{api_url}/users/{user_id}.json'
		
		response = requests.put(url, auth=HTTPBasicAuth(email, api_token), files=image_data)
		
		if response.status_code == 200:
			print(f"Successfully updated profile picture for user {user_id}")
		else:
			print(f"Failed to update profile picture for user {user_id}")

if __name__ == '__main__':
	# Step 1: Get all groups with 'unique_string' in the name
	unique_string_group_ids = get_unique_string_group_ids()
	
	if not unique_string_group_ids:
		print("No groups found with 'unique_string' in the name.")
		exit()

	# Step 2: Get all users in those groups
	users = get_users_in_groups(unique_string_group_ids)
	
	if not users:
		print("No users found in the specified groups.")
		exit()
	
	# Step 3: Update profile picture for each user
	for user in users:
		update_user_profile_picture(user['id'], image_path)
