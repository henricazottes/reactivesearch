<template>
	<div id="app">
		<ReactiveBase
			app="meetup_dataset"
			url="https://1e47b838a035:767b5a1a-03cb-4c5f-a536-4f399c24134b@arc-cluster-appbase-tryout-k8dsnj.searchbase.io"
			:enable-appbase="true"
		>
			<div class="row">
				<div class="col">
					<ToggleButton
						componentId="CitySensor"
						dataField="group.group_topics.topic_name_raw.keyword"
						:data="[
							{ label: 'Social', value: 'Social' },
							{ label: 'Adventure', value: 'Adventure' },
							{ label: 'Music', value: 'Music' },
						]"
					/>
				</div>
				<div class="col">
					<SelectedFilters componentId="CitySensor" />
					<ReactiveList
						componentId="SearchResult"
						dataField="group.group_topics.topic_name_raw.keyword"
						title="Results"
						sortBy="asc"
						class="result-list-container"
						:from="0"
						:size="5"
						:innerClass="{
							image: 'meetup-list-image',
						}"
						:pagination="true"
					>
						<div slot="render" slot-scope="{ data }">
							<ResultListWrapper>
								<ResultList
									v-bind:key="result._id"
									v-for="result in data"
									:href="result.event.event_url"
								>
									<ResultListImage :small="true" :src="result.member.photo" />
									<ResultListContent>
										<ResultListTitle>
											{{ result.member ? result.member.member_name : '' }} is
											going to
											{{ result.event ? result.event.event_name : '' }}
										</ResultListTitle>
										<ResultListDescription>
											{{ result.group ? result.group.group_city : '' }}
										</ResultListDescription>
									</ResultListContent>
								</ResultList>
							</ResultListWrapper>
						</div>
					</ReactiveList>
				</div>
			</div>
		</ReactiveBase>
	</div>
</template>

<script>
import './styles.css';

export default {
	name: 'app',
};
</script>

<style>
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
}
</style>
