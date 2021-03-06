Summary
-------
This module provides programatic access to the Convio Open API documented at http://open.convio.com/api/. It does not do anything on its own.

Based on the work originally done at http://drupal.org/project/convio_api, it has been updated for Drupal 7 and extended to support all APIs.

####Installation

* Enable the module
* Assign desired roles "administer convio api" permission
* Visit /admin/config/system/convio_api and configure with your API settings

####Example Usage

*Add a or update a constituent record - add an interest id and set their global accepts email flag*

    $params = array(
      'method' => 'createOrUpdate',
      'primary_email' => 'user@example.com',
      'email.accepts_email' => 'true',
      'email.preferred_format' => 'HTML',
      'add_interest_ids' => 1041
    );
    $response = convio_api_request($params, 'constituent', 'server');
    if ($response->code === '200') {
      //constituent was updated
    }
    else {
      //handle error
    }


*Get Team Caption Constituent Id from Teamraiser API*

    $params = array(
      'method' => 'getTeamsByInfo',
      'team_id' => 1080
    );
  
    $convio = convio_api_request($params, 'teamraiser', 'server');
    if ($response->code === '200') {
      $team = json_decode($response->data);
      return $team->getTeamSearchByInfoResponse->team->captainConsId;
    }
    else {
      //handle error
    }