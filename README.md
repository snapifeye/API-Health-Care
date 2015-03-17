<html>
	<head>
		<script type="text/javascript" src="http://events.snapifeye.com/snapifeye-widget/snapifeye-widget-all.min.js"></script>

		<style>
			html, body { margin: 0px; padding: 0px; }

			.sn-widget-gallery--info-container {
				display: inline-block !important;
				position: relative !important;
				width: 50% !important;
			}

			.dummy {
				margin-top: 100%;
			}

			.smarty {
				position: absolute;
				top: 0;
				bottom: 0;
				left: 0;
				right: 0;
			}

			.data-wrapper {
				position: absolute;
				width: 95%;
				height: 200px;
				top: 50%;
				margin-top: -150px;
				
			}
			.data-wrapper div {
				width: 95%;
				padding: 0px 75px;
			}
			
			.photo-meta-first-name,
			.photo-meta-last-name {
				font-style: italic;
				font-family: Helvetica;
				text-transform: uppercase;
				letter-spacing: 1px;

				color: #FFFFFF;
				font-weight: 600;
				font-size: 53px;
				line-height: 55px;
			}
			.photo-meta-last-name {
				margin-bottom: 25px;
			}
			.photo-question {
				font-style: italic;
				font-family: Helvetica;

				color: #FFFFFF;
				font-weight: 100;
				font-size: 36px;
				line-height: 43px;
			}

			.event-hash-tag {
				position: absolute;
				bottom: 200px;
				right: 50px;

				color: #FFFFFF;
				font-size: 36px;
				line-height: 43px;
				font-family: Helvetica;
			}
		</style>

		<script type="text/javascript">
			function resolveFirstName(photo) {
				var fullName = (photo.meta || {}).name;
				if (fullName) {
					fullName = fullName.split(" ")[0];
				}
				return fullName;
			}

			function resolveLastName(photo) {
				var fullName = (photo.meta || {}).name;
				if (fullName) {
					fullName = fullName.split(" ").pop();
				}
				return fullName;
			}

			function resolveQuestion1(data) {
				var questions = (data.event.offer_questions || []);
				for (var i = 0; i < questions.length; i++) {
					var question = questions[i];
					if (question.indexOf("name of") > -1) {
						return (data.photo.meta || {})[question]
					}
				}

				return null;
			}

			function resolveQuestion2(data) {
				var questions = (data.event.offer_questions || []);
				for (var i = 0; i < questions.length; i++) {
					var question = questions[i];
					if (question.indexOf("located") > -1) {
						return (data.photo.meta || {})[question]
					}
				}

				return null;
			}
			
		</script>

	</head>
	<body>

		<snapifeye-widget class="full-screen" params="eventId: 165, period: 7500, custom: true">
			<!-- This content inside of there is optional. This will customize the left side text -->
			<!-- Event object: $data.event -->
			<!-- Photo object: $data.photo -->
			<div class="dummy"></div>
			<div class="smarty">
				<div class="data-wrapper">
					<div class="photo-meta-first-name" data-bind="text: resolveFirstName($data.photo)"></div>
					<div class="photo-meta-last-name" data-bind="text: resolveLastName($data.photo)"></div>
					
					<div class="photo-question" data-bind="text: resolveQuestion1($data)"></div>
					<div class="photo-question" data-bind="text: resolveQuestion2($data)"></div>
				</div>
				
			</div>
                <div class="event-hash-tag"></div>
		</snapifeye-widget>

	</body>
</html>

